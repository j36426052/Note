# 開源專案

## 什麼是開源專案

參考[openSource Guide](https://opensource.guide/zh-hant/starting-a-project/)

**開源的意思**
當一個專案被開源，這意味着任何人都可以出於任何目的查看，使用，修改和分發你的專案。 這些權限通過開源許可強制實施。

**開源的目的**
個人或組織爲何想要開源一個專案，有各種各樣的的原因，例如：

- 協作： 開源專案可以接受世界各地人們的修改。 例如 Exercism 就是一個擁有350多個貢獻者的練習平臺。

- 採用和重組： 任何人幾乎可以出於任何目的使用開源專案。人們甚至可以使用它來構建其他東西。例如，WordPress 就是派生自一個名爲 b2 的現有專案。

- 透明度： 任何人都可以檢查開源專案是否有錯誤或不一致。 透明度對保加利亞 或美國等政府，銀行或醫療保健等受監管行業以及 Let’s Encrypt 等安全軟件都很重要。

## 開源專案的角色

- 作者: 專案的發起者或發起的社群
- 擁有者: 有權限直接修改程式碼或修改文件的管理員（不一定和作者是同一人）
- 維護者: 貢獻者，負責專案的方向和組織的管理（他們通常也是專案的作者或擁有者。）
- 貢獻者: 只要是爲專案做出了貢獻的人。
- 社群成員: 專案的使用者，他們有時會積極的參與討論或是表達他們對專案走向的看法。

## 常有的文件

- 許可協議（LICENSE）: 根據定義，每個開源專案都必須有個開源許可協議。如果專案沒有的話，那它不能算是個開源社群。
- README: README 是一個引導手冊，對剛加入社群的人們表示歡迎，它通常會解釋專案有何用處，為何發起，以及如何快速入門等。

以上兩者大部分都有

- 「COPYING」：此文件通常是用來說明專案的授權條款或版權聲明。它可以讓其他人知道如何合法地使用、修改或分發專案的代碼。
    有些專案也會使用LICENSE或NOTICE等其他名稱的文件來表達相同的目的12。
- 貢獻（CONTRIBUTING）: README 幫助人**認識**與**使用**專案，「貢獻」這個文件則是針對想對**專案貢獻**的人寫的指南。它會說明目前專案需要怎樣類型的貢獻者，並介紹貢獻時的流程是如何進行。並非所有的專案都會有這個文件，但如果有的話某種程度上也是向有意貢獻的人表達友善的意思。
- 行爲準則（CODE_OF_CONDUCT）: 這份文件裡頭設立了基本規範來約束參與者的行為以及提醒應有的禮儀，並非所有的專案都會有這個文件，但如果有的話某種程度上也是向有意貢獻的人表達友善的意思。
- 其它文件: 有些專案也許還有其它文件，例如教學、專案導覽，或者是管理政策，這在大型專案中常見。

## 專案討論

- （Issue tracker）: 這裡是人們討論專案相關問題的地方。
- 請求提取（Pull requests）: 這裡給人們檢查程式碼、以及相關問題的討論。


## License

參考[Choose an open source license](https://choosealicense.com/)，有三個大類別：

1. 用已經存在的專案繼續貢獻(I need to work in a community)
    通常是直接去看你想要延續的那個專案有甚麼License，可以從License、COPYING、READEME去找
2. MIT License

    MIT License是一種寬鬆的自由軟體授權條款，源自於麻省理工學院（MIT）。它的特別之處在於它只對再使用者提出了非常有限的限制，並且具有很高的授權相容性。使用MIT License的專案或代碼，可以被任何人自由地使用、複製、修改、合併、發佈、分發、再授權或出售，唯一的要求是必須在所有的複本或重要部分中包含版權聲明和許可聲明。此外，MIT License也允許在專有軟體中使用或整合MIT License的代碼，而不需要開放源代碼或支付費用。

3. GNU GPLv3

    根據網路搜尋結果，GNU GPLv3是一種自由軟體授權條款，它的特色在於它是一種強制性的copyleft授權，意味著使用GPLv3的軟體或代碼，必須在同樣的授權下發佈其修改版本或衍生作品，並且提供源代碼給使用者。GPLv3與前一個版本GPLv2相比，主要有以下幾個改進：

    - 防止tivoization：tivoization是指一些公司製造了運行GPL軟體的設備，但是通過硬體限制使得使用者無法安裝或運行修改過的軟體版本。GPLv3要求任何發佈GPL軟體的設備，必須提供安裝或運行修改版本所需的資訊或工具。
    - 防止禁止自由軟體的法律：一些法律（如美國的DMCA和歐盟的EUCD）規定破解或分享可以破解DRM（數位限制管理）的軟體是犯罪行為。這些法律不應該干涉GPL賦予使用者的權利。GPLv3明確規定，如果使用者在某個司法管轄區內無法合法地使用或分享GPL軟體，則該司法管轄區內的任何人都不能發佈或傳播該軟體。
    - 防止歧視性的專利協議：微軟曾經聲稱他們不會起訴自由軟體使用者侵犯專利，只要他們從支付微軟費用的供應商那裡獲得該軟體。這實際上是試圖收取自由軟體使用者的專利權利金，干涉了使用者的自由。GPLv3禁止任何人與這種協議合作，並且要求任何人如果收到這種協議的好處，必須將其延伸到所有GPL軟體使用者。

**MIT和GPLv3的差異**

- 如果你使用GPLv3的軟體或代碼，並且對其進行修改或衍生，然後發佈給其他人，你必須在同樣的GPLv3授權下提供源代碼，並且保留原來的版權和許可聲明。
- 如果你使用MIT License的軟體或代碼，你可以自由地修改或衍生，並且以任何形式發佈給其他人，無論是開源還是專有，只要你保留原來的版權和許可聲明。

GPLv3可以保護軟體或代碼的自由性，防止被封閉或私有化，但也限制了使用者的選擇和靈活性；而MIT License可以促進軟體或代碼的廣泛使用和傳播，但也可能導致自由軟體被轉化為專有軟體

## 貢獻別人的專案

好處以及原因：
- 鞏固現有技能
- 認識那些與你有相似興趣的人
- 互相溝通等等的
- 在公眾建立名聲

常見的貢獻方式：
1. 打Code：很常見，但又可以細分為重新設計、增加功能、deBug
2. 宣傳以及說明：例如用一個漂亮的突來說明一個專案
3. 說明文件：把Readme的東西
4. 規劃活動：有一個線下聚會之類的
5. 回答問題：幫忙回覆怎麼修Bug之類的

## 貢獻方式

參考[保哥文章](https://github.com/doggy8088/Learn-Git-in-30-days/blob/master/zh-tw/28.md)

參考[五倍紅寶石](https://gitbook.tw/chapters/github/pull-request)

根據網路搜尋結果，contributor和fork在GitHub裡面的差別在於：

- contributor是指一個對某個專案做出貢獻的人，貢獻的形式可以是提交代碼、修復錯誤、改進文件等。一個專案可以有多個contributor，他們可以是專案的擁有者、協作者或外部貢獻者。
- fork是指一個專案的分支，它是一個新的存儲庫，與原始的"上游"存儲庫共享代碼和可見性設置。fork通常用於在不影響原始專案的情況下進行修改或衍生，然後通過pull request將變更提議回上游存儲庫，例如在開源專案中或當一個人沒有上游存儲庫的寫入權限時。

因此，contributor和fork是不同層面的概念，一個人可以通過fork一個專案並提交pull request來成為該專案的contributor，也可以直接在原始專案上提交變更來成為contributor（如果有寫入權限）。

**pull request被接受之後，我會有哪些權限**
如果你的pull request被接受，你會成為該專案的contributor，但你不會自動獲得該專案的任何權限。你仍然只能在你自己的fork上進行修改，並且需要提交新的pull request來提議更多的變更。如果你想要直接在上游存儲庫上進行修改，你需要該專案的擁有者或協作者給你寫入權限或其他角色。不同的角色有不同的權限，例如讀取、寫入、管理等。具體的權限取決於該專案所屬的個人帳戶或組織的設置 。


## 找尋專案開始貢獻

直接看[這裡](https://opensource.guide/zh-hant/how-to-contribute/#%E6%89%BE%E5%B0%8B%E5%B0%88%E6%A1%88%E9%96%8B%E5%A7%8B%E8%B2%A2%E7%8D%BB)


## Star history

GitHub star有以下的意義：

- star是一種表示你對某個專案感興趣或支持的方式，你可以在GitHub上隨時查看你star過的專案，也可以在你的個人主頁上看到你star過的主題。
- star也可以幫助你發現相關或推薦的內容，在你的個人儀表板上，GitHub會根據你star過的專案或主題，向你推薦相似的專案或主題。
- star還可以表達對專案維護者的感謝和認可，許多GitHub上的專案排名都取決於專案的star數量，而Explore頁面也會根據star數量顯示熱門的專案。

https://star-history.com/#star-history/star-history&Date

好像是這個網站有東西啥的

## Sponce

方法：

GitHub 上的專案可以通過多種方式進行贊助，以下是一些常見的方法：

- GitHub 贊助（GitHub Sponsors）：
    GitHub 提供了一個內建的贊助平台，稱為 GitHub 贊助。通過註冊 GitHub 贊助，您可以讓其他使用者贊助您的專案，並為您的貢獻給予獎勵。GitHub 贊助支持多種支付方式，例如信用卡、PayPal 等，並且提供了方便的贊助管理和統計功能。
    參考[這篇](https://zhuanlan.zhihu.com/p/71035270)

- 第三方贊助平台：
    除了 GitHub 贊助外，還有許多第三方平台，如 Patreon、Open Collective、Liberapay、[Buy me a coffee](https://www.buymeacoffee.com/)等，提供了贊助和捐款的服務。您可以在這些平台上建立專案頁面，接受使用者的贊助和捐款。

- 自行設置贊助方式：
    您可以在您的專案頁面上提供您自己的贊助方式，例如註明您的 PayPal 或其他支付方式，並提供相應的資訊，以便使用者透過這些方式贊助您的專案。

- 捐款連結：
    您可以在您的專案中提供捐款連結，例如設置一個指向您設置的捐款頁面的連結，讓使用者可以通過這個連結進行捐款。

- 贊助特定功能或目標：您可以通過設置特定功能或目標的贊助計劃，吸引使用者贊助您的專案。例如，您可以設置一個目標金額，表示當達到這個金額時，您會釋放特定的功能或進行特定的改進。

**注意事項**

當在您的 GitHub 上放置贊助鏈接或圖標時，您應該遵從 GitHub 的規定，包括以下幾點：

- 放置位置和樣式：GitHub規定了放置贊助鏈接或圖標的位置和樣式。例如，您應該將贊助鏈接或圖標放置在個人或組織的主頁面上，並遵從 GitHub 提供的相關指引，如放置於頭像下方或概要資料區域。此外，樣式上應該符合 GitHub 的設計和風格要求，不得濫用顏色、圖標和樣式。

- 內容：贊助鏈接或圖標的內容應該與您的專案相符且合法合規。您應該確保贊助鏈接或圖標不包含任何違反法律法規、侵犯他人權利或違反 GitHub 政策的內容。此外，您應該清楚說明贊助的用途，例如資金將用於專案的開發、維護和改進等，並不得含糊不清或誤導性。您應該提供足夠的資訊，讓贊助者能夠明確了解他們的贊助將被用於何處。


## 加映

~~~python
from fastapi import FastAPI,Response
from typing import Union
import gradio as gr
import uvicorn
import os

app = FastAPI()

money1s = []
whichSide1s = []
money2s = []
whichSide2s = []

def batGradio(who,money1,whichSide1,money2,whichSide2):
    if (whichSide1 != None) & (whichSide2 != None):
        whos.append(who)
        money1s.append(money1)
        whichSide1s.append(whichSide1)
        money2s.append(money2)
        whichSide2s.append(whichSide2)
        return 'GooD'
    return 'Bad'

demo = gr.Interface(
    fn=batGradio,
    inputs= [
        gr.inputs.Textbox(lines=1, label="你的名字"),
        gr.inputs.Slider(0,5,step=1, label="下注多少"),
        gr.Radio(["會","不會"], label="是否及格"),
        gr.inputs.Slider(0,5,step=1, label="下注多少"),
        gr.Radio(["上","下"], label="會在預測分數的"),],
    outputs=gr.outputs.Textbox(label="Generated Text")
)
app = gr.mount_gradio_app(app, demo, path='/')

if __name__ == "__main__":
    uvicorn.run("main:app", host="0.0.0.0", port=3000, reload=True)
~~~

[專案本人](http://140.119.65.88:3000/)