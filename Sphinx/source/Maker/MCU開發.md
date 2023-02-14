# MCU開發.md

### 常見QA

**韌體和軟體學習上最大的差別?**

> 最大的差別就是軟體著重應用而韌體著重硬體訊號控制，並且軟體都是先假設底層韌體/硬體一切正常。韌體設計最根本的技術是”訊號處理”而不是程式。訊號處理意謂著你要先能理解兩個IC間的溝通方法，是否有依照IC DataSheet中的訊號時序圖來傳遞。”時序”表示訊號交握是有Timing的關係，這通常是軟體背景者最難入手的地方，如果你已經拿著會動的Code去改,那只有學到軟體的功夫而不是韌體的真本事。艾鍗課程講師會教授每一位學員LA邏輯分儀如何使用並搭配艾鍗在Windows上開發的訊號產生工具，讓學員可以用一目了然的方法去看見波形時序是怎麼一回事。

**Arduino與MCU**



## 參考資料
[基於ARM-M0架構開發](https://ithelp.ithome.com.tw/users/20141979/ironman/4820)
[MCU付錢課程](https://www.ittraining.com.tw/ittraining/index.php/course/firmware/pic)
[Arduino vs MCU](https://jimsun-embedded.blogspot.com/2019/01/arduino-mcu.html)

2主要看他對MCU的介紹就好