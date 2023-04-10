# handwrite.md

## 簡介

主要是寫最簡單的深度學習範例：手寫辨識，的程式碼結構講解。


## 結構

我們主要把它分為四個部分

1. 匯入資料
2. 資料整理以及資料標準化
3. 建立Model以及訓練
4. 評估Model


## 程式碼

**匯入套件**
~~~py
import numpy as np
from keras.models import Sequential
from keras.datasets import mnist
from keras.layers import Dense, Dropout, Activation, Flatten
from keras.utils import np_utils  # 用來後續將 label 標籤轉為 one-hot-encoding
from matplotlib import pyplot as plt
~~~

**匯入資料**
~~~py
(X_train, y_train), (X_test, y_test) = mnist.load_data()
~~~

它是一個tuple，再深一層是numpy.ndarray

**資料整理以及資料標準化**
~~~py
 # 將 training 的 label 進行 one-hot encoding，例如數字 7 經過 One-hot encoding 轉換後是 0000001000，即第7個值為 1
y_TrainOneHot = np_utils.to_categorical(y_train)
y_TestOneHot = np_utils.to_categorical(y_test)
 # 將 training 的 input 資料轉為2維
X_train_2D = X_train.reshape(60000, 28*28).astype('float32')
X_test_2D = X_test.reshape(10000, 28*28).astype('float32')
x_Train_norm = X_train_2D/255
x_Test_norm = X_test_2D/255
~~~

**建立Model以及訓練**
~~~py
 # 建立簡單的線性執行的模型
model = Sequential()
 # Add Input layer, 隱藏層(hidden layer) 有 256個輸出變數 784 = 28*28
model.add(Dense(units=256, input_dim=784, kernel_initializer='normal', activation='relu'))
 # Add output layer
model.add(Dense(units=10, kernel_initializer='normal', activation='softmax'))
 # 編譯: 選擇損失函數、優化方法及成效衡量方式
model.compile(loss='categorical_crossentropy', optimizer='adam', metrics=['accuracy'])

train_history = model.fit(x=x_Train_norm, y=y_TrainOneHot, validation_split=0.2, epochs=10, batch_size=800, verbose=2)
~~~

**評估Model**
~~~py
 # 顯示訓練成果(分數)
scores = model.evaluate(x_Test_norm, y_TestOneHot)
print("\t[Info] Accuracy of testing data = {:2.1f}%".format(scores[1]*100.0))
~~~

## 超級拆解篇

先看[這個](https://blog.csdn.net/baoxin1100/article/details/107917633)
是train_on_batch的介紹

kerasF&Q[這裡](https://keras.io/getting_started/faq/#how-can-i-use-keras-with-datasets-that-dont-fit-in-memory)

接下來主要照著以下兩個做

官方API[這裡](https://keras.io/api/models/model_training_apis/)
官方範例[這裡](https://www.tensorflow.org/guide/keras/writing_a_training_loop_from_scratch)
(目前)


## 進階啟動區

建立requirement.txt
~~~requirement
numpy
keras
tensorflow
pika
~~~

建立Docker file
~~~dockerfile
FROM python:3.9-buster

WORKDIR /app

COPY . /app

RUN apt-get update

RUN apt-get install nano

RUN pip install -r requirements.txt

CMD python3 step2.py
~~~



建立container
~~~
docker run --link rabbitmq:rabbitmq -v D:\Program\Python\rabbitmq\step2:/app -v D:\Program\Python\rabbitmq\volumn\Data:/Data --name step2 worker
~~~

容器互聯參考[這裡](https://philipzheng.gitbook.io/docker_practice/network/linking)

## 老師補充篇

**關於資料**

Q1: 為什麼要把資料分成 (X_train, y_train), (X_test, y_test)
A1: 參下面這張表

|  X區域   | Y區域  |
|  ----  | ----  |
| X_train  | y_train |
| X_test  | y_test |

Q2: 為什麼要做 onehot 這件事情
A2: 因為我們在做的是一個預測類別(category)的事情，所以不應該預測出來一個數字是介於2~3之間之類的

Q3: 為什麼要把資料reshape
A3: 因為原本的資料是圖片，因此是二維的，但為了符合A1的表格，因此要把它打平

Q4: 為什麼要把資料除以255
A4: 因為原始的資料有灰階的問題，假如是白色的話都是255，因此矩陣原本都是落在0~255之間的數字。但我們希望算出一個介於0~1之間的數字，因此要把它除以255。

> onehot注意事項：假如直接使用np_utils.to_categorical()這個函數，那它的category不一定如你所料，例如1可能會變成[0,0,0,0,1]之類的，而不是[0,1,0,0,0]

**建立Model篇**

Q1: 為什麼model是用Sequential()
A1: 這個只是tensorflow的名稱而已，它指的是由左到右一條線的深度學習

Q2: 增加隱藏層時，那些參數分別是甚麼意思
A2:
- units         指的是這一層神經元的數目
- input_dim     指的是一筆input的資料有幾個dimention
- activation    非線性優化函數，常見的有softmax, relu等等

Q3: 為什麼網路上的範例，最後一層都沒有softmax
A3: 因為它們在選擇loss function的時候，是塞一個物件，而且那個物件有一個參數是from_logits，預設關閉，打開就會自動加一個softmax上去，可以參考[這裡](https://www.tensorflow.org/api_docs/python/tf/keras/losses/SparseCategoricalCrossentropy)

Q4: 為什麼官網上有三種crossentropy
A4: 主要是為了不同的input資料所準備

- [SparseCategoricalCrossentropy](https://www.tensorflow.org/api_docs/python/tf/keras/losses/SparseCategoricalCrossentropy#get_config)：會自動幫你做category
- [BinaryCrossentropy](https://www.tensorflow.org/api_docs/python/tf/keras/losses/BinaryCrossentropy)：輸入資料是Binary
- [CategoricalCrossentropy](https://www.tensorflow.org/api_docs/python/tf/keras/losses/CategoricalCrossentropy)：預設你已經onehot進去了

Q5: fit裡面的參數分別是甚麼意思
A5:
- validation_split： 指的是把整個資料分為多少比例當作測試用
- epochs：這坨資料要訓練幾次，例如原本有8萬筆要跑的資料，那假如設定10，那就會變成80萬筆
- batch_size：一次調整weigh要丟多少筆資料進去

Q6: 資料要不要隨機打散
A6: 通常會自己做一遍，不過fit函數的shuffle=True可以把它打開。

> 老師建議：就算原本就是打開的，那shuffle，

## 常用的Layer的東西

~~~python
model.add(Dense(30, name='Layer12'))
~~~


## 參考資料

1. [蔡炎龍的python 課程](https://ctld.video.nccu.edu.tw/media/1023)

第二章主要有手寫資料的介紹，比較冗一點點就是了

2. [Mediun隨便找的](https://sweetornotspicymarathon.medium.com/tesorflow-keras-%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E6%96%B0%E6%89%8B%E4%B8%80%E5%AE%9A%E8%A6%81%E7%8E%A9%E7%9A%84mnist%E6%89%8B%E5%AF%AB%E6%95%B8%E5%AD%97%E8%BE%A8%E8%AD%98-9327366cc838)

比較大方向的介紹

3. [iThome 文章](https://ithelp.ithome.com.tw/articles/10191404)

註解看起來寫的比較詳細
