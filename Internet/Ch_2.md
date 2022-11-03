# Chapter 2. Application Layer

## 2.1 Priciples of Network Applications


## 2.2 The Web and HTTP


## 2.3 Electronic Mail in the Internet


## 2.4 DNS-The Internet's Directory Service


### 其他補充

**如何註冊DNS**
> 跟域名管理公司買 e.g. Go Daddy
> 並且要有一個固定IP 或者 有其他服務可以一直更新

## 2.5 Peer-to-Peer File Distrubution
Note: 以上其他的東西都是Server-Client 的設計

**特色**
- 每多一個Peer，整個網路就更強大
- 兩千年的時候比較火紅
- 假如打電話要通過很遠，會用P2P連線（但用P2P其他人就沒辦法監控打多久之類的）

### 傳輸效率
(參考老師投影片)

**Client-Server**
情境：將伺服器上傳一個檔案的資料量寫作$F$,上傳速率寫作$u_S$，總共有$n$位使用者，其下載速度為$d$,最慢的那位寫做$d_{min}$

- 理論速度$D_{C-S} \geq \max\{NF/u_S,F/d_{min}\}$ 

**P2P**

$D_{P2P} \geq \max\{F/u_S,F/d_{min},NF/(u_S + \sum u_j)\}$

這邊要注意的是最慢那位$F/d_{min}$之中的$F$是很多份小chunks，並且每個小chunks都來自於不同人

而$NF/(u_S + \sum u_j)$的部分是因為整個系統的人都可以做上傳這件事情。

### Others

BitTorrent, 一個檔案P2P服務提供者，他有一個tracker(server)去知道大家的資訊，讓你知道可以跟誰$P2P$





## 2.6* Video Streaming and Content Distribution Networks
（老師沒講）

## 2.7* Socket Programming: Creating Network Applications
（老師沒講）
