# GUI.md

查了一下說推薦使用pyQt

~~~python
if self.mylineedit.text() != '':
            self.mybutton.setText(self.mylineedit.text())
~~~


## 輸入框(QPlainTextEdit)相關

取得文字

~~~py
self.plainTextEdit.toPlainText()
~~~

設定文字

~~~py
self.plainTextEdit.setPlainText()
~~~

## 按鈕相關
~~~py
self.mybutton.clicked.connect(self.onButtonClick)
~~~

替代function

~~~py
    def onButtonClick(self):
        outputText = self.inputField.toPlainText()
        outputText = outputText.replace(self.subField.toPlainText(),self.toField.toPlainText())
        self.outputField.setPlainText(outputText)
~~~

## 參考資料

[pyQt教學入門](https://jason-chen-1992.weebly.com/home/python-ui-pyqt)

裡面主要是講解一開始安裝和介面，沒有太多method 介紹

[]()


# 定義一下按按鈕的void