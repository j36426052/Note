# dockerSetup.md

## Introduction

> 這份文件主要記錄關於畢業專題，把整個專案架構弄好的一個說明文件，主要是用docker把以下圖片的架構分別裝好，再用composer把它組起來

**先備知識**

1. 先知到Docker Compose相關


**小筆記**

- 假如container啟動失敗，用docker logs [containerName]來檢查一下

- 假如需要把資料夾丟進去docker裡面，先用sudo chmod 777 * 修改一下權限

## 建立Prometheus, Node exporter 以及 Grafana

這個部分的安裝，主要希望使用docker-compose自動建立上述三個container，並且事先寫好各自的設定檔案以便互相串接，假如對於docker-compose不熟可以參考：

其中有幾個好處：
1. 一勞永逸，把東西設定好之後，只要按下docker-compose 就可以把所有container上線
2. 網路方便，使用docker-compose會建立docker網路，container之間不需要使用ip繞來繞去，直接用container name當作ip互相溝通

### Prometheus

**簡介**

Prometheus主要是Time Series的資料庫，在這次的重點是當作其他container以及grafana的橋樑，讓其他container的資訊先彙整到prometheus裡面，接著grafana再跟promethues拿取資料


**參考資料：**
[架設普羅米修斯(0)](https://ithelp.ithome.com.tw/articles/10269989)

我們直接使用Docker-compose的方式建立container，因此先建立一個docker-compose.yml的檔案，並且在裡面寫上

~~~yml
version: "3.8"
services:
  prometheus:
    image: prom/prometheus:v2.30.0
    volumes:
      - ./prometheus/config:/etc/prometheus
      - ./prometheus/data:/prometheus
    ports:
      - 9090:9090
~~~

其中volumes在local上的檔案結構為：

~~~
prometheus/
├── config
│   └── prometheus.yml
└── data
~~~

其中，promethues.yml主要設定跟其他container架接的情況，等等建立node exporter會更改裡面的內容

### Node exporter
參考 [架設普羅米修斯(1)](https://ithelp.ithome.com.tw/articles/10270805)

在這邊一樣使用同一份docker-compose.yml檔案，並在裡面的service加上以下的資訊，以加上node-exporter這個container

~~~yml
node-exporter:
  image: prom/node-exporter:v1.2.2
  restart: unless-stopped
  volumes:
    - /proc:/host/proc:ro
    - /sys:/host/sys:ro
    - /:/rootfs:ro
  command: 
    - '--path.procfs=/host/proc'
    - '--path.rootfs=/rootfs'
    - '--path.sysfs=/host/sys'
    - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    - '--no-collector.arp'
    - '--no-collector.netstat'
    - '--no-collector.netdev'
    - '--no-collector.softnet'
~~~


接著，我們要對prometheus裡面的prometheus.yml裡面加上node exporter這個target:

~~~yml
scrape_configs:
  - job_name: node
    static_configs: 
      - targets: ["node-exporter:9100"]
~~~


基本上就大功告成

> 可以注意到targets裡面我們是使用node-exporter當作名字，這是docker-compose的功勞

### Grafana

[建立Grafana教學](https://ithelp.ithome.com.tw/articles/10272141)

同上，一開始先在docker-compose.yml裡面新增關於grafana:這個container的相關資訊：



~~~
grafana:
  image: grafana/grafana:8.1.5
  restart: unless-stopped
  volumes:
    - ./grafana/provisioning:/etc/grafana/provisioning
  ports: 
    - 3000:3000
~~~

這邊介紹一下grafana內部的結構，在/etc/grafana/provisioning裡面，可以設定兩個重要的東西

~~~
|-- provisioning
        |-- dashboards
        |   `-- dashboard.yml
        `-- datasources
            `-- datasource.yml
~~~

1. datasources<br>
主要是用來紀錄資料來源，在這邊我們設定普羅米修斯當作資料來源就好
2. dashboards<br>
主要用來紀錄有沒有預載的dashboard

因此我們在docker compose的資料夾裡面新增grafana/provisioning，並且在docker-compose.yml 裡面，放入

~~~
volumes:
  - .grafana/provisioniog:/etc/grafana/provisioning
~~~

為了啟動就客制化自己的grafana，我們把一些設定先寫進兩個yaml裡面。

參考的資料有：
[客制化yaml](https://medium.com/swlh/easy-grafana-and-docker-compose-setup-d0f6f9fcec13) ，裡面給了上述的結構圖，以及
[promethus](https://github.com/vegasbrianc/prometheus/blob/master/grafana/provisioning/datasources/datasource.yml)的datasource設定

基本上datasource的設定就把上面的東西拷貝下來就好

**dashboards**

首先，先複製一下客制化yaml裡面的dashboards的yml

~~~yaml
# config file version
apiVersion: 1

providers:
# <string> an unique provider name
- name: My Dashboard
  # <int> org id. will default to orgId 1 if not specified
  org_id: 1
  # <string, required> name of the dashboard folder. Required
  folder: ''
  # <string, required> provider type. Required
  type: 'file'
  # <bool> disable dashboard deletion
  disableDeletion: false
  # <bool> enable dashboard editing
  editable: true
  # <int> how often Grafana will scan for changed dashboards
  updateIntervalSeconds: 5
  # <bool> allow updating provisioned dashboards from the UI
  allowUiUpdates: true
  options:
    # <string, required> path to dashboard files on disk. Required
    path: /etc/grafana/provisioning/dashboards
    # <bool> use folder names from filesystem to create folders in Grafana
    foldersFromFilesStructure: true
~~~


在這之中，只要在意倒數三行的path就好，裡面存放你欲設想要的dashboard，我們可以先在
[這裡](https://grafana.com/grafana/dashboards/)

找到你喜歡的模版，並且下載它的json檔案

接著把它放到你指定的位子，基本上就大功告成

~~~
|-- provisioning
        |-- dashboards
        |   `-- dashboard.yml
        |   `-- json here!!!!!!
        `-- datasources
            `-- datasource.yml
~~~

在Node exporter裡面，我們使用的是[這個模版](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)

### RabbitMQ

參考
1. [官方網站看不懂](https://www.rabbitmq.com/prometheus.html)
2. [隨便一篇](https://opensource.dwins.com/?p=463)
3. [酷酷乾貨](https://blog.51cto.com/erdong/4844362)
4. [官方自己定義的dashboard](https://github.com/rabbitmq/rabbitmq-server/tree/main/deps/rabbitmq_prometheus/docker/grafana/dashboards)

5. [就這篇了](https://lework.github.io/2019/12/24/rabbitmq-monitor/)
6. [docker compose設定](https://x-team.com/blog/set-up-rabbitmq-with-docker-compose/)

先把Rabbit MQ pull 下來

一樣把相關的設定寫進去docker composer

~~~
rabbitmq:
  image: rabbitmq:3-management-alpine
  container_name: 'rabbitmq'
  ports:
      - 5672:5672
      - 15692:15692
  volumes:
      - ~/.docker-conf/rabbitmq/data/:/var/lib/rabbitmq/
      - ~/.docker-conf/rabbitmq/log/:/var/log/rabbitmq
~~~

如果要手動啟用exportor，輸入

```
rabbitmq-plugins enable rabbitmq_prometheus
```

但我們沒有這麼做，參考[這個](https://github.com/docker-library/rabbitmq/issues/260)

在docker compose裡面加入
```
volumes:
    - "./rabbit_enabled_plugins:/etc/rabbitmq/enabled_plugins"
```   
並且加上檔案rabbit_enabled_plugins
```
[rabbitmq_prometheus]
```   

接著跟node exporter一樣，把設定檔加在普羅米修斯的檔案裡面，接著再設定grafana



### Python






