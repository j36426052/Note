# Docker 程式課教學


## 安裝

**Windows 安裝**

直接到官網下載Docker Desktop來安裝，基本上一直下一步就可以。

*打開時遇到問題*

參考 [這個](https://bbs.huaweicloud.com/blogs/359540)

控制台 --> 程式與功能 --> 啟用或關閉 windows 功能 --> 啟用windows 的Linux 子系統

**Mac 安裝**

(待補)


## Docker 概念講解

還記得以前我們在寫python時，假如我們要做數據分析下載了pandas，到了新的電腦的時候，我們就需要再下載一次，而且有時候會有版本不同的問題。

為了解決這個問題，最直覺的方法是：把整個pandas`打包`起來，直接丟到另一台電腦上，而Docker就是實現它的一種方法，打包的東西我們稱為Image，執行Image的東西稱為Container，Image就像是有個職位裡面會描述工作內容以及提供職業所需要的工具，Container是上班的人


## 基本(常用)指令

> 這邊 windows可以用powershell 來執行 docker 相關的指令

常用指令(執行在終端機)：
~~~docker
docker search [IMAGE wnat to search] # 找找酷酷docker
docker pull [IMAGE want to download] # 把docker下載下來
docker image    #察看目前所有image*
docker ps       #察看目前運行的container(想看全部加上 -a)*
~~~

## 啟動兩個Image

MySQL 啟動
~~~bash
docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql:5.7.24
~~~

phpMyAdmin 啟動

~~~bash
docker run --name phpmyadmin -d --link mysql -e PMA_HOST="mysql" -p 8080:80 phpmyadmin/phpmyadmin
~~~

- --name 代表docker container 的名稱
- -d --link 代表想要連結容器的名字
- -e 設定一些環境變數
- -p 設定 port 之類的

## SQL 概念講解

SQL可以想像成Excel的樣子一列一欄的方格，主要用來儲存資料，下一堂課會有更多的介紹。

## SQL + python

**phpMyadmin 簡單操作**


這邊使用 pymysql 來對資料庫做一些事情


**建立連線**

~~~python
import pymysql
import logging

def connectDb(dbName):
    try:
        mysqldb = pymysql.connect(
                host="127.0.0.1",
                user="root",
                passwd="123456",
                database=dbName)
        return mysqldb
    except Exception as e:
        logging.error('Fail to connection mysql {}'.format(str(e)))
    return None
~~~

**建立Table**

在創建表之前，我們要首先了解 MySQL 中的數據類型，MySQL 中主要包括以下六種數據類型

- `INT`: 所有的整數
- `DECIMAL(M, N)`: 實數，`M` 表示有效位數，`N` 表示小數位數
- `VARCHAR(l)`: 長度為 `l` 的字符串
- `BLOB`: 二進制的大對象，存儲大數據
- `DATE`: 日期格式，`YYYY-MM-DD`
- `TIMESTAMP`: 時間戳，`YYYY-MM-DD HH:MM:SS`

SQL講解：
假設我們建一個 student 表，包括 student_id、name、major，其中 student_id 是主鍵。則我們可以用以下代碼來創建表
~~~sql
CREATE TABLE student (
    student_id INT PRIMARY KEY,
    name VARCHAR(20),
    major VARCHAR(20)
);
~~~



python範例
~~~python
conn = connectDb('school')
cur = None
if conn is not None:
    cur = conn.cursor()
if cur is not None:
    sql = 'CREATE TABLE `teacher`( \
    `TEACHER_ID` INT(2), \
    `FIRST_NAME` VARCHAR(20) \
    `LAST_NAME` VARCHAR(20), \
    `AGE` VARCHAR(2)\
    )'
    cur.execute(sql)
~~~

**插入資料**

SQL講解：
通過 INSERT INTO 在表中插入數據。
~~~sql
INSERT INTO student VALUES (1, 'Quicy', 'Mathematic');
~~~

python範例
~~~python
conn = connectDb('school')
cur = None
if conn is not None:
    cur = conn.cursor()
if cur is not None:
    sql = 'INSERT INTO `school`.`teacher` (`TEACHER_ID`, `FIRST_NAME`, `LAST_NAME`, `AGE`) VALUES (1, \'TOM\', \'LEE\', 25)'
    cur.execute(sql)
    conn.commit()
~~~

**查詢資料**
SQL講解：
通過 SELECT * FROM table; 可以獲取名為 table 的表的所有數據。但我們通常並不是很想獲取全部的數據，如果我們只想獲取某一些列的數據，那將查詢語句中的 * 更改為對應的屬性即可

~~~sql
SELECT student.name, student.major FROM student;
~~~

python範例
~~~python
    conn = connectDb('world')
    cur = None
    if conn is not None:
        cur = conn.cursor()
    sql = 'select * from city'
    if cur is not None:
        cur.execute(sql)
        result_one = cur.fetchone()
        result_many = cur.fetchmany(5) #獲取5筆記錄
        resultall = cur.fetchall()
        print 'Fetch one row:'
        print result_one[1] #數字代表對應column, 由0開始，即0=第一column
        print '\nFetch many(5) rows:'
        for row in result_many:
            print row[1] #數字代表column
        print '\nFetch all rows:'
        for row in resultall:
            print row[1] #數字代表column
~~~

**更新和刪除資料**
SQL講解：
對於已經插入的數據，我們可能需要更新某一條或多條記錄的內容，通過 UPDATE 語句可以實現更新數據。

~~~
UPDATE student SET major = 'Biology' WHERE name = 'Jack';
~~~

上述代碼表示將 `student` 表中名字是 `Jack` 的這條記錄的 `major` 更改為 `Biology`。

通過 `DELETE FROM` 語句可以實現刪除數據

~~~
DELETE FROM student WHERE name = 'Jack';
~~~

python範例：

~~~py
conn = connectDb('school')
cur = None
if conn is not None:
    cur = conn.cursor()
if cur is not None:
    sql = 'UPDATE TEACHER SET AGE=28 WHERE TEACHER_ID=1'
    cur.execute(sql)
    conn.commit()
~~~

~~~py
if __name__ == '__main__':
conn = connectDb('school')
cur = None
if conn is not None:
    cur = conn.cursor()
if cur is not None:
    sql = 'DELETE FROM TEACHER WHERE TEACHER_ID=1'
    cur.execute(sql)
    conn.commit()
~~~

## 今日小挑戰

在上一次，我們有IOS系統上AppStore與app有關的資料，請建立一個適合的Table，將其中的一些資料手動key進去

(假如覺得太簡單可以把"所有"資料自動跑進去)

## 參考資料

1. [IT Home phpMyAddmin + MySQL](https://ithelp.ithome.com.tw/articles/10200754)
2. [pymysql操作mysql database](https://zcgnotes.com/python-%E4%BD%BF%E7%94%A8pymysql%E6%93%8D%E4%BD%9Cmysql%E6%95%B8%E6%93%9A%E5%BA%AB-create-table-select-insert-update-delete/)