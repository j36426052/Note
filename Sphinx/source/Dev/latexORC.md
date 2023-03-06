# LatexORC.md

這邊主要來找一些東西是怎麼跑的

## 現成工具區
1. [EasyScreenOCR](https://easyscreenocr.com/?lang=zh-hant)
2. [Mathpix](https://mathpix.com/)

## 論文閱讀區

### Historical Review of OCR Research and Development

主要可以把OCR分成Template-Matching Methods 還有 Structure Analysis Method

前者主要擅長電腦字，代表的方法有projection（從二維變一維）還有peelhole，後者則比較彈性

以下則是一些Approach

**Template Matching Approach**

1. Applicaiton Matching Approach
2. Normalization
3. Karhunen-Loeve Expansion
4. Series Expansion
5. Feature Matching
6. Nonlinear Template Matching
7. Graphical Matching

**Struture Analysis Approach**

1. Thinning Line Analysis
2. Bulk Decomposition
3. Stream Following Analysis
4. Vectorization
5. Contour Following Analysis

### PDF2LaTeX: A Deep Learning System to Convert Mathematrical Documents from PDF to LaTeX

主要就是非常直接了當的把整個系統是怎麼跑的，以及其中的一些concern還有解決方法打上去

**主要架構**

1. PPC(Projection Profile Cutting)
    - Column detection
    - Line detection
    - Token detection
2. CNN Classifier
3. Conditional Random Field
4. Neural Translators
    - Math translator
    - Plaintext translator

**PPC**
在這個區域，我們主要利用Projection來確定一些事情

首先，要知道整篇文章是單欄還是雙欄，遇到的問題是有可能會有標題列，因此要用low-pas filter(LPF)的方法，來優化整個函數

接著，我們要把每個column拆成line，主要是用水平的projection，其中會遇到一些問題

1. Overlapped lines：例如有個上標(次方之類的)，卡到上面那一行，導致兩行被當作一行，這個時候去計算多數的行高來解決
2. Variable hats：帽子被當作單獨一行
3. Fraction expressions：分數被分成兩行
4. Binding variables：sum的上面和下面

最後，我們把每一行再做拆解，把它拆成一個一個字(token)

**CNN Classifier**
現在，我們有了一大堆的Token，我們要先判斷它是個文字(plainText)還是數學符號

**Conditional Random Field**

主要是用來把上面的Classifier做後處理

**Neural Translators**

本篇重點，還沒看。

## 參考資料

在資料夾 OCRfile 裡面

1. [deep learning and OCR](https://neptune.ai/blog/building-deep-learning-based-ocr-model)

2. [把pdf變成圖片](https://levelup.gitconnected.com/4-python-libraries-to-convert-pdf-to-images-7a09eba83a09)

3. [把圖片變成pdf](https://datatofish.com/images-to-pdf-python/)

4. [python 圖片處理](https://ithelp.ithome.com.tw/articles/10226578)