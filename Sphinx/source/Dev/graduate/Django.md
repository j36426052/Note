# Django.md

Django主要是一個Python的後端，相比於FastAPI、Flask功能更為完整，詳細可以看[這邊的介紹](https://developer.mozilla.org/zh-TW/docs/Learn/Server-side/Django/Introduction)

## 初次建立

先參考[這邊(IT鐵人)](https://ithelp.ithome.com.tw/users/20111829/ironman/1804)的步驟

1. 安裝Django
~~~bash
pdm add django
~~~
2. 建置project
~~~bash
django-admin startproject graduate
~~~
3. 運行測試
~~~bash
python manage.py runserver
~~~
4. 建立一個功能
~~~bash
python manage.py startapp [app_name]
~~~
5. 改裡面的viewer
~~~python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def index(request):
    return HttpResponse('This is a test')
~~~

關於功能的[介紹](https://ithelp.ithome.com.tw/articles/10199933)

6. 把return改成retrn html

先在app名稱資料夾底下建立templates資料夾，並且在裡面放html出來

參考[這裡](https://developer.mozilla.org/zh-TW/docs/Learn/Server-side/Django/Home_page)

> 注意，要把app放進setting 裡面的 INSTALLED_APPS中



