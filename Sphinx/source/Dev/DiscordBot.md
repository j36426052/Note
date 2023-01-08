# Discord機器人

總之主要參考第一個參考連結，並且使用他們自家的docker image(gorialis/discord.py)

## 隨機點餐

為了讓dictionary能夠隨機選擇，所以把字典先變成list，接著再使用random來把東西弄一弄。

參考 [這篇](https://bobbyhadz.com/blog/python-get-random-key-value-from-dictionary)


## 使用docker 加上 python 套件

[參考這裡](https://ithelp.ithome.com.tw/articles/10256857)

## docker file裡面設定要安裝的python東西


~~~
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


## 參考資料

1. [用docker部屬python機器人](https://www.vultr.com/docs/how-to-run-a-python-discord-bot-on-a-docker-application/)
2. [python bot教學](https://hackmd.io/@kangjw/Discordpy%E6%A9%9F%E5%99%A8%E4%BA%BA%E5%BE%9E0%E5%88%B01%E8%B6%85%E8%A9%B3%E7%B4%B0%E6%95%99%E5%AD%B8)
3. [Docker File教學](https://ithelp.ithome.com.tw/articles/10191016)
4. [建立私人docker registry](https://ithelp.ithome.com.tw/articles/10191213)