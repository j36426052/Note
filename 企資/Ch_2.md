# Chapter 2. Application Layer

## 2.1 Priciples of Network Applications

### 2.1.1 Network Application Architectures

### 2.1.2 Processes Communicating

### 2.1.3 Transport Services Available to Applications

### 2.1.4 Transport Services Provided by the Internet

### 2.1.5 Application-Layer Protocols

### 2.1.6 Network Applications Covered in This Book

## 2.2 The Web and HTTP

### 2.2.1 Overview of HTTP

### 2.2.2 Non-Persistent and Persistent Connections

### 2.2.3 HTTP Message Format

### 2.2.4 User-Server Interaction: Cookies

### 2.2.5 Web Caching

## 2.3 Electronic Mail in the Internet

### 2.3.1 SMTP

### 2.3.2 Mail Message Formats

### 2.3.3 Mail Access Protocols

## 2.4 DNS-The Internet's Directory Service

### 2.4.1 Services Provided by DNS

### 2.4.2 Overview of How DNS Works

### 2.4.3 DNS  Records and Messages

### 2.4.4 其他補充

**如何註冊DNS**
> 跟域名管理公司買 e.g. Go Daddy
> 並且要有一個固定IP 或者 有其他服務可以一直更新

## 2.5 Peer-to-Peer File Distrubution
Note: 以上其他的東西都是Server-Client 的設計

**特色**
- 每多一個Peer，整個網路就更強大
- 兩千年的時候比較火紅
- 假如打電話要通過很遠，會用P2P連線（但用P2P其他人就沒辦法監控打多久之類的）

### 2.5.1 傳輸效率
(參考老師投影片)

**Client-Server**
情境：將伺服器上傳一個檔案的資料量寫作$F$,上傳速率寫作$u_S$，總共有$n$位使用者，其下載速度為$d$,最慢的那位寫做$d_{min}$

- 理論速度$D_{C-S} \geq \max\{NF/u_S,F/d_{min}\}$ 

**P2P**

$D_{P2P} \geq \max\{F/u_S,F/d_{min},NF/(u_S + \sum u_j)\}$

這邊要注意的是最慢那位$F/d_{min}$之中的$F$是很多份小chunks，並且每個小chunks都來自於不同人

而$NF/(u_S + \sum u_j)$的部分是因為整個系統的人都可以做上傳這件事情。

### 2.5.2 Others

BitTorrent, 一個檔案P2P服務提供者，他有一個tracker(server)去知道大家的資訊，讓你知道可以跟誰$P2P$


## 2.6* Video Streaming and Content Distribution Networks

### 2.6.1 Internet Video

### 2.6.2 HTTP Streaming and DASH

### 2.6.3 Content Distrubution Networks

### 2.6.4 Case Studies: Netflix and Youtube

## 2.7* Socket Programming: Creating Network Applications

### 2.7.1 Socket Programming with UDP

### 2.7.2 Socket Programming with TCP

## 2.8 Summary


