# GUI.md

主要使用pyQt，優點是UI設計可以用GUI的方式拖一拖，並且有一個良好的架構的時候，重新設計UI不用重新來一遍。

## 流程

1. 首先會使用Qt Designer 這款軟體來設計UI，儲存會得到一個.ui的檔案
2. 接著使用python套件pyuic5，執行以下指令，就可以得到一個UI的執行檔案
~~~
pyuic5 -x demo.ui -o demo_ui.py
~~~
3. 設定一個 controller.py，來控制裡面的Button函數
4. 再設定一個程式進入點，來執行 controller.py

## 程式進入點

主要是把controller這個物件建立出來，並且用show來搞定
~~~ py
if __name__ == '__main__':
    import sys
    app = QtWidgets.QApplication(sys.argv)
    window = MainWindow_controller()
    window.show()
    sys.exit(app.exec_())
~~~

## Controller 寫法
**建構子**

把UI裡面的東西new出來，並且用self.ui來選擇UI裡面中的元件
~~~py
def __init__(self):
        super().__init__() # in python3, super(Class, self).xxx = super().xxx
        self.ui = Ui_LaTexTool()
        self.ui.setupUi(self)
        self.setup_control()
~~~

**setup_control**

主要設定每一個元件裡面的功能
~~~py
def setup_control(self):
        # 按鈕設定區
        self.ui.subButton.clicked.connect(self.subButtonClick)
        self.ui.matrixButton.clicked.connect(self.matrixButtonClick)
~~~

### 元件設定

**QPlainTextEdit(輸入框)**

取得文字

~~~py
self.ui.plainTextEdit.toPlainText()
~~~

設定文字

~~~py
self.ui.plainTextEdit.setPlainText()
~~~

**Button按鈕**
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

[pyQt架構](https://ithelp.ithome.com.tw/articles/10268341)

把整個分成start.py, controller.py, ui.py

[pyQt美化相關](https://www.google.com/url?sa=t&source=web&rct=j&url=https://zhuanlan.zhihu.com/p/390192953%3Futm_id%3D0&ved=2ahUKEwi_xIWlgbb9AhXWr1YBHSGXDGIQFnoECA0QAQ&usg=AOvVaw09gsD2nNXdo9FPdIf5ja5-)
