# Discord機器人

## 程式架構

一開始進入的地方
~~~py
 #導入Discord.py
 import discord
 import random
 #client 是我們與 Discord 連結的橋樑，intents 是我們要求的權限
 intents = discord.Intents.default()
 intents.message_content = True
 client = discord.Client(intents=intents)
~~~

設定發言等等（主要改這邊）
~~~py
 #調用event函式庫
@client.event
 #當機器人完成啟動時
async def on_ready():
    print('目前登入身份：',client.user)

@client.event
 #當有訊息時
async def on_message(message):
    #排除自己的訊息，避免陷入無限循環
    if message.author == client.user:
        return
    #取得使用者說的東西以及發送訊息
    if message.content.startswith('說'):
        await message.channel.send("你要我說什麼啦？")
~~~
執行區
~~~py
client.run('TOKEN') #TOKEN在剛剛Discord Developer那邊「BOT」頁面裡面
~~~

## 使用docker 加上 python 套件

[參考這裡](https://ithelp.ithome.com.tw/articles/10256857)

整個資料夾裡面會有以下的檔案
1. DiscordBot.py        (程式主要的檔案)
2. Dockerfile           (設定DockerImage的環境)
3. requirements.txt     (該Docker要裝哪些python套件)

### Build Docker Image

在資料夾中執行以下的指令，就可以把這個Image建立起來

~~~docker
docker image build -t <喜歡的image name> .
~~~
其中.代表dockerfile在當前的資料夾

**docker file**

~~~dockerfile
FROM python:3.9-buster

WORKDIR /app

COPY . /app

RUN apt-get update

RUN apt-get install nano

RUN pip install -r requirements.txt

CMD python3 main.py
~~~

FROM： 使用到的 Docker Image 名稱，今天使用 CentOS

MAINTAINER： 用來說明，撰寫和維護這個 Dockerfile 的人是誰，也可以給 E-mail的資訊

RUN： RUN 指令後面放 Linux 指令，用來執行安裝和設定這個 Image 需要的東西

ADD： 把 Local 的檔案複製到 Image 裡，如果是 tar.gz 檔複製進去 Image 時會順便自動解壓縮。Dockerfile 另外還有一個複製檔案的指令 COPY 未來還會再介紹

ENV： 用來設定環境變數

CMD： 在指行 docker run 的指令時會直接呼叫開啟 Tomcat Service

**requirement.txt**
畢竟整個DiscordBot不用太多套件，所以就打這個就好
~~~
discord
~~~




## 參考資料

1. [用docker部屬python機器人](https://www.vultr.com/docs/how-to-run-a-python-discord-bot-on-a-docker-application/)

他們的Docker image 太肥了

2. [python bot教學](https://hackmd.io/@kangjw/Discordpy%E6%A9%9F%E5%99%A8%E4%BA%BA%E5%BE%9E0%E5%88%B01%E8%B6%85%E8%A9%B3%E7%B4%B0%E6%95%99%E5%AD%B8)
3. [Docker File教學](https://ithelp.ithome.com.tw/articles/10191016)
4. [建立私人docker registry](https://ithelp.ithome.com.tw/articles/10191213)