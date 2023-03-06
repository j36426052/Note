# exe.md
安装pyinstaller
首先安装pyinstaller，使用安装命令：pip3 install pyinstaller，如下图所示。


pyinstaller -F setup.py


## 儲存檔案在exe檔案裡面

~~~py
from tkinter import filedialog
path_to_pref = filedialog.asksaveasfilename(initialfile="example.tex",defaultextension='.tex',initialdir = "./",title = "Select file",filetypes = [("tex files","*.tex")])
        if path_to_pref != '':
            with open('./example.tex','r', encoding='UTF-8') as f:
                a = f.read()
            with open(path_to_pref,'w', encoding='UTF-8') as f:
                f.write(a)
~~~

## 打包txt之類的

打包的時候變成

~~~cmd
pyinstaller --add-data 'pptset.tex;.' --add-data 'example.tex;.' -F start.py
~~~

然後使用的時候

~~~py
a = str(pkgutil.get_data( __name__, 'pptset.tex' ).decode('utf-8'))
~~~

就可以讀取到檔案

[參考文章](https://zhuanlan.zhihu.com/p/162237978)