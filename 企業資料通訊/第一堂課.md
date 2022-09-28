# ㄧ. 網路簡介

## 常見角色
* Host(End system): TV, gaming consoles, server ...
* communication links: coaxial cable, copper wire, radio spectrum
* packet weitches: routers, link-layer switches.
* 上面那些都是硬體
* Internet Service Providers (ISPs)
* Internet standards
    * developed by the Internet Engineering Task Force (IETF)
    * called requests for comments (RFCs)

**Definition.**
A protocol defines the format and the order of messages exchanged between two or more communication entities, as well as the actions tacken on the transmission and/ or recepipt of a message or other event.

## 常見家用網路連接方法

1. DSL(digital subscriber line)  
    * 跟電話線同一條
    * 頻率如下
        * 0 - 4 kHz 電話（類比）
        * 4 - 50 KHz 上傳（數位）
        * 50 KHz - 1MHz 下載（數位）
    * splitter: 在家裡面，把訊號分給電話和DSL modem（把數位類比分開）
    * DSL modem: 拿來上網的東西
    * CO: 大本營 (local central office)
    * DSLAM: 大本營裡面拿來分開數位和類比的  
    (digital subscriber line access multiplexer)
    > ADSL 實際上很慢，因此現在台灣的ADSL其實是VDSL，用兩條電話線來達到飛快的網路體驗

    ![DSL](./figure/DSL.png)
2.  Cabel Internet Access
    * From the same company that provides its cable television.
    * hybrid fiber coax (HFC)
        * because both fiber and coaxial cable are emplyed in this system
    * cable modem termination system (CMTS)
        * divide HFC network into two channels(上傳和下載)
    * have coordinate transmissions and avoid collisions.

3. FTTH (fiber to the home)
    * two competing optical-distribution network architectures.
        * AONs: active optical networks.
        * PONs: passive optical networks.
    
4. 5G fixed wireless
5. Ethernet and Wifi
6. Wide-Area Wireless Access
    * 3G, LTE(Long Term Evolution) 4G, 5G

## 連接網路的媒介
分類方法
* guided media: 固體的, e.g. fiber-optic cable, twisted-pair copper wire, coaxinal cable
* unguided media: wireless LAN, satellite channel.

1. Tiwsted-Pair Copper Wire
    * least expensive, commonly used guided medium
    * been used by telephone networks.
    * consists of two insulated copper wires, each about 1 mm thick, arranged in a regular spiral pattern (To reduce electrical interference)
    * Unshielded Twisted Pair (UTP)
2.  Coaxial Cable
    * consists of two copper conductors but are concentric
    * common in cable television systems
    * shared medium
3. Fiber Optics
    * thin, flexible, conduct, pulese of light
    * prefered long-haul guided transmission media, e.g. overseas links
    * high cost of opticals devices, e.g. transmitters, receivers, switched
4. Terrestrial Radio Channels
    * in electromagnetic spectrum
5. Satellite Radio Channels
    * geostation satellites
    * low-earth orbiting (LEO) satellites (closer to earth)

## Moving Data
這邊簡介該資料傳輸的兩個方法

1. packet switching
2. circuit switching
    * a connection between the sender and the receiver
    * frequency-division multiplexing (FDM): frequency spectrum of a link is divided up among the connections established accross the link
    * time-division multiplexing(TDM)

**Compare Packet Switching v.s. Circuit Switching**

| Packet Switching | Circuit Switching|
|----|----|
|better sharing of transmission capacity|less delay|
|efficient and less costly||
|more user in a time||


## Network of Network
To let global user to use Internet, we need lots of fundemental structure an different level design to reduce the cost.

1. Network Structure 1
    * interconnect all of the access ISPs with a single global transit ISP.
    * Consider: If it's profitable, by economic, will appear another global ISP who wants compete with origin one.
2. Network Structure 2
    * consists of the hundreds of thousands of access ISPs and multiple global transit
    * the global transit ISPs themseleves must interconnect.
3. Network Structure 3
    * In reality, because no one can converge everywhere we have geginal ISP, and it connect to tier-1 ISP (like imaginary global ISP)
    * More real, it may exist bigger erginal ISP and small reginal ISP
4. Network Structure 4
    * PoP(points of presence) is simply a group of one or more rounters (at the same location) in the provider's network where customer ISPs can connect into the provider ISP.
    * multi-home: Any ISP connect to two or more reginal ISP further more T1-ISP
    * peer: they can directly connect their networks together so that all the traffic between them passes over the direct connection rather that through upstream internediaries.
    * Internet Exchange Point(IXP): a meeting point where multiple ISPs can peer together.
5. Network Structure 5
    * add the content-provider networks e.g. Google

## Types of Delay

1. Processing Delay
    * examine the packet's header, ...
2. Queuing Delay
    * waits to be transmitted onto the link
3. Transmission delay
    * $\dfrac{L}{R}$ 
4. Propagation Delay
    the data limit in phisic
5. End-to-end Delay
    * $d_{\text{end-end}} = N(d_{proc} + d_{trans} + d_{prop})$

**Throughput**
 > * instantaneous throughput  
 the rate at which Host B is receiving file
 > * average throughput  
 $\dfrac{F}{T}$ (bits/sec)  where $F$ is file bit, $T$ is total second.

 ## Five-layer Internet protocol stack (top-down)

 1. Application Layer
 * e.g. HTTP protocol, SMTP, FTP
 * refer to this packet of information at the application layer as a message
 2. Transport Layer
 * e.g. TCP, UDP
 * thinked as segement
 3. Network Layer
 * e.g. IP
 * thinked as datagrams
 4. Link Layer
 * thinked as frames
 5. Physical Layer

 **Encapsulation**
<span style = "color:red"> picture P82 </span>

## Internet Attack

**Dos(denial-of-service) attack**

* Three Clacess
    * Vulnerability attack
        * let target host get a "well-crafted" messages, the service can stop or host crash
    * Bandwidth flooding
        * send lots of file to host
    * Connection flooding
        * establish a large number connection
* DDos = Distributed DoS

> *Note:* packet sniffer: a passive receiver that records a copy of every packet that files. 
