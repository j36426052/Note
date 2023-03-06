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




## 參考資料

1. [蔡炎龍的python 課程](https://ctld.video.nccu.edu.tw/media/1023)

第二章主要有手寫資料的介紹，比較冗一點點就是了

2. [Mediun隨便找的](https://sweetornotspicymarathon.medium.com/tesorflow-keras-%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-%E6%96%B0%E6%89%8B%E4%B8%80%E5%AE%9A%E8%A6%81%E7%8E%A9%E7%9A%84mnist%E6%89%8B%E5%AF%AB%E6%95%B8%E5%AD%97%E8%BE%A8%E8%AD%98-9327366cc838)

比較大方向的介紹

3.[iThome 文章](https://ithelp.ithome.com.tw/articles/10191404)

註解看起來寫的比較詳細
