# GPT

## Introduction

這週主要看看有哪些基於Python + GPT的工具，目前有以下的候選人

1. [ChatGPT Python SDK](https://github.com/labteral/chatgpt-python)
2. [EASYChatGPT](https://github.com/AIGCT/EASYChatGPT)
3. [chatgpt_academic](https://github.com/binary-husky/chatgpt_academic)

## [chatgpt_academic](https://github.com/binary-husky/chatgpt_academic)

主要是幫助弄論文相關的

### 如何使用

### 技術總結

首先看一下它的檔案內容，有幾個基本的先提一下：
1. .gitattributes：是一個 Git 的設定檔，可以指定在對 repository 進行操作時的一些行為和選項，例如指定不同類型的檔案如何處理、如何進行 diff 等等。
2. .gitignore：要求git不要丟到網路上的東西
3. Dockerfile：用來建立Image的東西
4. LICENSE：可以參考[這篇IThome](https://ithelp.ithome.com.tw/articles/10231751)的說明
5. README：用來顯示在Github點進去的說明
6. version：

> 通常情況下，版本文件是一個純文本文件，用於記錄軟體或專案的版本號、版本名稱、發布日期等信息，以便用戶、開發者和其他利益相關方在需要的時候查詢。版本文件的具體格式和內容可能因專案而異，但通常包含以下信息：

- 版本號：通常是由幾個數字和點號組成的一個字串，用來標識軟體或專案的版本。
- 版本名稱：通常是一個簡短的、易於理解的名稱，用來描述該版本的主要特點或重點。
- 發布日期：該版本的發布日期，可以是具體的日期和時間，也可以是一個區間。
- 其他信息：可能包括版本更新的概述、修復的問題列表、新功能列表、依賴關係等。
- 版本文件的存在可以幫助開發者和用戶快速了解軟體或專案的版本狀態，以及該版本的主要更新內容。在開發過程中，版本文件還可以幫助開發團隊更好地管理和控制版本，以確保不同版本的一致性和穩定性。

7. requirements.txt：紀錄Python文件裡面有用到甚麼套件，裡面有：

~~~python
gradio>=3.23
requests[socks]
transformers
python-markdown-math
beautifulsoup4
latex2mathml
mdtex2html
tiktoken
Markdown
pygments
pymupdf
openai
numpy
~~~

這邊就先不一一來看了，有空再說，歡迎大家從別人的requirement來觀察自己想要學一些什麼。

**程式進入點**

觀察Readme就可以發現開始程式碼的進入點也是 main.py，沒有特別炫酷

~~~python
import os; os.environ['no_proxy'] = '*' # 避免代理网络产生意外污染
import gradio as gr
from request_llm.bridge_chatgpt import predict
from toolbox import format_io, find_free_port, on_file_uploaded, on_report_generated, get_conf, ArgsGeneralWrapper, DummyWith
~~~

**gradio**

Gradio是一個Python套件，提供一個簡單易用的介面，用戶可以藉由這個介面快速地建立、分享和使用機器學習模型（看起來好像不限制於機器學習，一個白癡東西也可以把它弄得很漂亮，可以研究看看）。以下是Gradio主要的功能和應用：

1. 快速地部署和分享機器學習模型：Gradio提供了一個簡單的界面，讓用戶可以快速地部署和分享自己的機器學習模型。用戶只需要使用少量的程式碼，就可以在網頁上建立一個可交互的介面，讓其他人可以使用自己的模型。

2. 支援多種輸入和輸出類型：Gradio支援多種不同類型的輸入和輸出，包括圖片、文本、音頻、視訊和數值。用戶可以在介面上選擇輸入和輸出類型，並且對應到自己的模型。

3. 輕鬆地進行模型比較和選擇：Gradio支援同時顯示多個不同的模型，讓用戶可以輕鬆地進行模型比較和選擇。用戶可以在介面上切換不同的模型，並且即時地查看輸出結果。

4. 可以嵌入到其他應用中：Gradio可以輕鬆地嵌入到其他應用中，比如說Flask或Django等Web框架。用戶可以在其他應用中引用Gradio，並且快速地建立可交互的機器學習介面。

5. 易於使用和定製：Gradio提供了一個簡單易用的API，讓用戶可以快速地建立自己的介面。同時，Gradio也提供了許多不同的配置選項，讓用戶可以自由地定製自己的介面。

總的來說，Gradio是一個方便易用的工具，可以讓用戶快速地部署、分享和使用自己的機器學習模型。Gradio的功能和應用也非常廣泛，可以應用於各種不同的機器學習領域。


其中request_llm.bridge_chatgpt, toolbox
可以藉由觀察，知道它是開發者自己寫的東西，有需要我們再過去觀察

觀察以下程式碼：
~~~python
from core_functional import get_core_functions
functional = get_core_functions()

    # 基础功能区的回调函数注册
    for k in functional:
        click_handle = functional[k]["Button"].click(fn=ArgsGeneralWrapper(predict), inputs=[*input_combo, gr.State(True), gr.State(k)], outputs=output_combo)
        cancel_handles.append(click_handle)
~~~
可以看到，程式是藉由這一行來將函數放到button上面，酷吧，所以當我們要了解每一個按鈕它的用處，那我們就需要跑到core_functional這個地方去弄。


## [EASYChatGPT](https://github.com/AIGCT/EASYChatGPT)

可以看見requirement非常簡潔，只有revChatGPT這個東西

> revChatGPT是一個用於與OpenAI的ChatGPT API進行交互的輕量級Python套件。它使用了反向工程的官方API，並支持多行輸入和編輯歷史輸入等功能。

https://github.com/davincee/revChatGPT

那我們到程式進入點 app.py 看看：
~~~python
from bbot import run


if __name__ == '__main__':
    run()
~~~
很明顯是叫我們去bbot裡面找函數

接著來到 bbot.py 觀察：
~~~python
from revChatGPT.Official import Chatbot
from config import getToken
openai_key = getToken()

chatbot = Chatbot(api_key=openai_key) #初始化chatgpt


def run():

    # 打印蓝色字迹的输出
    print("\033[1;33m" +
          "遇到报错优先考虑重新运行" + "\033[0m \n")
    input_text = ""

    while input_text != "quit":

        # 打印蓝色字迹的输出
        print("\033[1;34m" + "你的 输入: " + "\033[0m")
        input_text = input()

        out = chatbot.ask(input_text)
        # 打印绿色字迹的输出
        print("\033[1;32m" + "ChatGPT 输出: " + "\033[0m")
        # 打印输出
        print(out["choices"][0]["text"])
        # 黄色分割线
        print("\033[1;33m" +
              "-----------------------------------------" + "\033[0m")


if __name__ == "__main__":
    run()
~~~

可以看見，它做的就只是接收指令還有print它的output而已，確實是EASYChatGPT

## [ChatGPT Python SDK](https://github.com/labteral/chatgpt-python)

觀察一下它的requirement，只有tls_client（用來網路通訊加密用的）還有rich（提供了許多用於美化命令行輸出的工具和函數，例如顏色、文本格式化、進度條、表格等等。使用 rich 可以讓命令行輸出更加美觀、易讀、易於理解。）

在觀察一下chatgpt-python裡面有一個 \_\_init\_\_.py ，它文件是 Python 套件或模塊的初始化文件，通常包含用於初始化套件或模塊的代碼，是 Python 程序中非常常見的文件之一。

大魔王看起來就是其中的[chatgpt.py](https://github.com/labteral/chatgpt-python/blob/master/chatgpt/chatgpt.py)了，由於它是套件，可以發現它只由def一大堆東西，想要鑽研哪個功能那就去看指定的def

另外，可以看到整個套件有用到class、def \_\_init__這些東西，有物件導向的味道