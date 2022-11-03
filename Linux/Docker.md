# Docker 教學

## 安裝


### 常見錯誤（讓未來更方便）


## 新手上路

找找酷酷docker
~~~Docker
docker search [IMAGE wnat to search]
~~~
把docker下載下來
~~~Docker
docker pull [IMAGE want to download]
~~~

## 常用指令
**察看目前所有image**
~~~Docker
docer image
~~~
**察看目前運行的container(想看全部加上 -a)**
~~~Docker
docker ps 
~~~
**新建Container(有名字的那種)**
~~~Docker
docker run -it --name [ContainerName] [IMAGE] 
~~~
**啟動Container(ubuntu image要在run的時候加上-it才不會爆炸)**
~~~Docker
docker start [ContainerName]
~~~
**進入到Container**
~~~
docker exec -it [ContainerName] [Command]
~~~
通常command輸入/bin/bash

**關掉Container**
~~~Docker
docker stop [ContainerName]
~~~
**刪除Container**
~~~Docker
docker rm [ContainerName]
~~~




## 參考資料
1. [Docker](https://github.com/twtrubiks/docker-tutorial)
2. [合併Docker-Dockerfile](https://ithelp.ithome.com.tw/articles/10187192)
