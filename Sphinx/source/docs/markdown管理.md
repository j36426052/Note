# Markdown管理

### Introduction

內容主要是介紹在這麼多的Markdown裡面，該怎麼管理，並且有好看的瀏覽介面。

## Gitpage + Hexo


優點：可以
缺點：要public的才可以分享


參考教學：
1. [一個hack md 的文件](https://hackmd.io/@Heidi-Liu/note-hexo-github)



## SPHINX

1. [官網](https://www.sphinx-doc.org/en/master/)
2. [教程](https://zhuanlan.zhihu.com/p/264647009)
3. [參考toc](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html)
4. [參考toc(中文)](https://catx4.gitbooks.io/ossf_epaper_collection/content/APP/Apps-201307-Sphinx.html)



一開始要裝的東西（用mac裝，我全部改成用homebrew）

~~~bash
sudo apt install git
sudo apt install make
sudo apt install python3
sudo apt install python3-pip
pip3 install -U Sphinx
pip3 install sphinx-autobuild
pip3 install sphinx_rtd_theme
pip3 install recommonmark
pip3 install sphinx_markdown_tables

~~~

先在桌面建立一個Sphinx資料夾，terminal進到裡面之後執行 sphinx-quickstart

接著回答五個問題

1. 分離來源並建立資料夾：是
2. 專案名成
3. 作者姓名
4. 專案發布版本
5. 專案語言：zh_TW

建立完之後的結構：
~~~
--Makefile
--build
--make.bat
--source
  --_static
  --_templates
  --comf.py
  --index.rst
~~~

* Makefile：可以看作是一个包含指令的文件，在使用 make 命令时，可以使用这些指令来构建文档输出。
* build：生成的文件的输出目录。
* make.bat：Windows 用命令行。
* _static ：静态文件目录，比如图片等。
* _templates：模板目录。
* conf.py：存放 Sphinx 的配置，包括在 sphinx-quickstart 时选中的那些值，可以自行定义其他的值。
* index.rst：文档项目起始文件。

### 1. 建立html

在目錄執行make html, 就會在 bulid/html 目錄產生html相關文件

可以用sphinx-autobuild啟動HTTP伺服器

~~~
sphinx-autobuild source build/html
~~~

### 2. 修改主題

打開 conf.py，找到html_theme, 修改成sphinx_rtd_theme，就會變很漂亮

### 3. 支援Markdown

原本不支援，但可以透過recommonmark來支援，如果需要支持表格還要另外裝 sphinx-markdown-tables 插件。這兩個插件前面已經裝好了，要在conf.py 裡面增加擴展的支援。

~~~
extensions = [
  'recommonmark',
  'sphinx_markdown_tables'
]
~~~

### 4. 支援LaTeX(待補)


### 5. 常用方法

**index.rst**
這個算是個目錄檔，原始碼顯示詳細
~~~
# 首頁名稱
=================== #分隔線

.. toctree:: # 用來生成目錄的
   :maxdepth: 1 #顯示目錄的深度多少
   :glob:       #可以使用*符號

   *            #顯示這個資料夾所有的檔案
   Dev/index    #顯示Dev資料夾內的index檔案


~~~

基本上在每個資料夾都放一個index，假如那層資料夾裡面有東西就寫個*符號

### 6. 丟到Github + read

1. 丟到github，然後在gitignore裡面把build/加進去
2. 註冊 [read the docs](https://readthedocs.org/)
3. 在丟到read the docs之前，記得在根目錄加上requirment.txt, 把extensions裡面的東西加進去
4. 丟上read the docs, 大功告成




> 修改完conf.py之後都要執行一次make html



## MakeFile

好像是讓它自己產生文件，我也看不太懂

1. [教學文件](https://www.cnblogs.com/npyx/articles/12331145.html)


