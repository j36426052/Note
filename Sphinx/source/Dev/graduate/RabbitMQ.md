# RabbitMQ 開發文件

## 閱讀心得

建議先從2開始看，主要是在講原理沒有程式碼

裡面安裝使用

> docker run --name rabbitmq -d -p 15672:15672 -p 5672:5672 rabbitmq:management

其中15672是web管理介面的port，預設帳號密碼是 guest

接著參考第五個參考文件

基本上用Docker打開的那個Image是RabbitMQ的Server

假如想要建立Comsumer或者Producer的話，那就再開幾個Python的Docker來處理事情。


## Example

## 參考文件

1. [簡單講解RabbitMQ的原理(推薦看2，比這個詳細)](https://zamhuang.medium.com/rabbitmq-%E4%BA%94%E5%88%86%E9%90%98%E8%BC%95%E9%AC%86%E4%BA%86%E8%A7%A3-rabbitmq-%E9%81%8B%E4%BD%9C-fcaecbaa69d4)
2. [基本介紹 + 推薦Docker image](https://kucw.github.io/blog/2020/11/rabbitmq/)
3. [Message Queue介紹 + 小範例](https://ithelp.ithome.com.tw/articles/10238631)
4. [官方網站Hello World教學](https://www.rabbitmq.com/tutorials/tutorial-one-python.html)
5. [20分鐘學Docker Rabbitmq](https://www.architect.io/blog/2021-01-19/rabbitmq-docker-tutorial/)

