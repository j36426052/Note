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

## Django串gradio

為了在Django中使用Gradio，您需要在Django的views.py中導入gradio，並創建一個gr.Interface實例。然後，您需要在urls.py中添加一個路徑，將其連接到gr.Interface實例的get\_launch\_page方法。最後，您需要在settings.py中添加gradio到INSTALLED\_APPS列表[<sup>[2]</sup>](https://www.runoob.com/python3/python-ai-draw.html)。

以下是一個簡單的例子，展示了如何在Django中使用Gradio來實現一個圖像分類模型：

> 備註，記得安裝 pdm add setuptools

views.py
~~~python
import gradio as gr import torch from torchvision
import transforms import requests from PIL
import Image

model = torch.hub.load('pytorch/vision:v0.6.0', 'resnet18', pretrained=True).eval()
response = requests.get('https://git.io/JJkYN')
labels = response.text.split('\\n')

def predict(inp):
     inp = Image.fromarray(inp.astype('uint8'), 'RGB')
     inp = transforms.ToTensor()(inp).unsqueeze(0) with torch.no_grad():
      prediction = torch.nn.functional.softmax(model(inp)[0], dim=0)
      return {labels[i]: float(prediction[i]) for i in range(1000)}

inputs = gr.inputs.Image()
outputs = gr.outputs.Label(num_top_classes=3)
interface = gr.Interface(fn=predict, inputs=inputs, outputs=outputs)

def index(request):
    return interface.get_launch_page(request)
~~~
urls.py
~~~python
from django.urls import path from . import views

urlpatterns = [ path('', views.index, name='index'), ]
~~~
settings.py
~~~python
INSTALLED_APPS = [ … 'gradio',]
~~~