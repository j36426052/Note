# ESP32設定

## VSCode Setting

我們直接轉行跑到micro-python去開發爽啦

**來自GPT的建議**

以下是使用 Micropython 開發 ESP32 的具體安裝步驟：

1. 到官方下載 Micropython 固件
2. 安裝 esptool.py（燒錄用的）
3. 燒錄 Micropython 固件到 ESP32
4. 連接到 ESP32
5. 在 ESP32 上運行 Micropython
6. 開始使用 Micropython 開發 ESP32

安裝可以參考[這個](https://jimirobot.tw/esp32-micropython-tutorial-burn-binfile-103/)

會直接跑到安裝韌體的步驟

GetStart[這裡](https://github.com/pycom/pymakr-vsc/blob/HEAD/GET_STARTED.md)





## GPT分析篇

1. MicroPython
優點：

- 易於學習和使用，使用Python語言和庫可以快速開發ESP32應用程序
- 支持REPL，可以快速進行調試和測試
可以輕鬆地控制ESP32的各種硬件功能
缺點：

運行速度比C/C++編譯的程序慢
沒有直接訪問ESP32硬件的庫和API

2. Arduino IDE
優點：

- 易於學習和使用，使用Arduino語言和庫可以快速開發ESP32應用程序
- 支持豐富的Arduino社區和庫
- 可以輕鬆地控制ESP32的各種硬件功能
缺點：

- 開發過程中需要在Arduino IDE中編寫和編譯C++代碼，可能需要一些額外的學習成本
- 在開發大型應用程序時，可能需要進行更多的調試和測試
Visual Studio Code + PlatformIO
優點：

- 提供了豐富的庫和示例
- 具有良好的跨平台支持和自動化工具
- 支持多種微控制器和開發板
缺點：

- 安裝和設置過程可能需要一些額外的學習成本
- 在開發小型應用程序時，可能會感覺過於複雜

Espressif IoT Development Framework (ESP-IDF)
優點：

- 提供了豐富的API和庫，可以直接訪問ESP32硬件
- 具有豐富的示例和文檔，可以快速上手
- 可以達到較高的性能
缺點：

- 學習曲線比較陡峭，需要較多的C語言編程知識
- 在開發小型應用程序時，可能會感覺過於複雜

綜合來看，每種ESP32開發方式都有其優點和缺點。在選擇開發方式時，需要根據自己的技術水平、開發需求和個人偏好進行評估和選擇。