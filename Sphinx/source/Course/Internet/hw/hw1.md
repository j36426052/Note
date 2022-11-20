# 企業資料通訊作業一
109306058 資管三 康瑋翔

## Q1: What are the pros and cons of ADSL and cable access network?

||ADSL|Cable|
|---|---|---|
|Pros|1. 在台灣、大多數住家已經有電話線<br>使用此方案不用多拉線<br>2. 連線寬頻穩定，不用跟別人搶|1.從社區附近的電信箱連回central office只要一條線，<br>因此成本低廉且維護容易|
|Cons|1. 因為電話線的硬體限制，<br>若只用一條電話線寬頻較慢|1. 由於訊號是社區附近共用一條，<br>因此在尖峰時間寬頻會比較小|

## Q2: What are the pros and cons of wired and wireless network?

||Wired Network|Wireless Network|
|---|---|---|
|Pros|連線穩定，ping值以及寬頻都比無線來得好|在需要多裝置使用網路時佈線方便|
|Cons|若有多裝置需求，線路布置較為麻煩|由於是利用電磁波作為介質，因此容易<br>被其他電波（微波爐等等）或者其他網路互相干擾|

## Q3: What is the reason why application messages must be fragmented

> 「實際」上，可以故意設定不切成小的封包傳送，但「實務」上不會這麼做，原因是當我們選擇  
將訊息切成一小塊一小塊後，在同一個時間內，可以讓不同的使用者同時交換訊息，而不用一直  
等待某一個人傳送完資料後，才能開始傳送自己的東西，並且當某一些封包消失時，只要傳送其  
消失的部分，不用整個檔案都重新傳輸。

## Q4: Assume an ISP deploys routers along with Taiwan's High-Speed Rail train stations (total 12 stations, i.e., 11 hops), and the total length of the railroad is 349.5 KM. How long (in seconds) does it task for a packet of length 1,000 bytes to propagate over these fiber links (the fiber propagation speed is $2.5 \times 10^8$ m/s and the transmission rate is 10Gbps)

>在這個題目我們考慮兩種Delay:
>
>1. Propagation Delay:藉由公式$\dfrac{d}{s}$  
>將數字帶入得到$\frac{349.5 \cdot 1000}{2.5 \cdot 10^8} = 0.001398$(秒)
>    
>2. Transmission delay:藉由公式$\dfrac{L}{R}\cdot n$  
>將數字帶入得到$\frac{1000}{10\cdot 10^9} \cdot (12-1) = 11 \cdot 10^{-7}$
>
>因此整筆資料傳完的時間為 $11 \cdot 10^{-7} + 0.001398$秒

## Q5. We plan to develop an in-game VoIP service over a packet-switched network. Assume the analog voice signals are converted to a digital 64 kbps bit stream on the fly and voice sender then groups the bits into 56-byte packets. Assume Internet bandwidth is 100 Mbps on the average and its average propagation delay is 100 msec. How long (in seconds) does it take for you to wait for a voice response from your friend? Is there any other possible delay? Please list them as more as possible.

> 1. $\dfrac{64 + 56}{100 \cdot 10^6} + 0.1$
> 2. 麥克風到電腦的時間（用藍芽會很慢）、傳送的queueing delay、遊戲收到資料之後美化聲音的時間

## Q6 Suppose users share a 3 Mbps link. Also suppose each user requires 150 kbps when transmitting, but each user transmits only 10 percent of the time.

a. When circuit switching is used, how many users can be supported?  

> $\dfrac{3 \cdot 10^6}{150 \cdot 10^3} = 20$ （人） （同時使用）

b. For the remainder of this problem, suppose packet switching is used. Find the probability that a given user is transmitting.  


> 可以假設一個時段$t$，而用戶只會有$\dfrac{t}{10}$的時間在傳輸資料，因此發現用戶正在傳送資料的機率便是$\dfrac{t}{10} / t = \dfrac{1}{10}$

c. Suppose there are 120 users. Find the probability that at any given time, exactly n users are transmitting simultaneously.(Hint: binomial distribution.)  

> 使用二項式分布公式$\left(\begin{matrix}n \\ k\end{matrix}\right) p^k(1-p)^{n-k}$，其中$n=120,k=n,p=0.1$  
>我們得到$\left(\begin{matrix}120 \\ n\end{matrix}\right) p^k(1-p)^{n-k} = \dfrac{120!}{n!(120-n)!}0.1^{n}0.9^{120-n}$

d. Find the probability that there are 21 or more users transmitting simultaneously.

>使用卜瓦松分佈近似（$\lambda = np = 120\cdot 0.1 = 12$）並使用其累積分布函數$$e^{-\lambda}\sum^{k}_{i=0}\dfrac{\lambda^i}{i!} = 0.9884$$
> 得知$20$人以下使用的機率為$0.9884$再用全機率 $1 - 0.9884 = 0.0116 = 1.16\%$
