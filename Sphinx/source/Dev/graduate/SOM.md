# SOM.md

全名：Self-Organising Map

老師說是目前唯一一個Deep Learning中的非監督式學習

參考：[這裡](https://towardsdatascience.com/understanding-self-organising-map-neural-network-with-python-code-7a77f501e985)


## Bing聊天給我的

導入所需的庫
~~~python
import numpy as np
import matplotlib.pyplot as plt from minisom
import MiniSom from sklearn.datasets
import fetch_openml
~~~

載入MNIST數據集
~~~python
X, y = fetch_openml('mnist_784', version=1, return_X_y=True)
X = X / 255.0 * 2 - 1
 # 將數據歸一化到[-1,1]區間
~~~
定義SOM的參數
~~~python
som_shape = (30, 30)
 #輸出層的形狀
input_len = X.shape[1]
 #輸入層的長度
sigma = 1.0
 #鄰域函數的標準差
learning_rate = 0.5
 #學習率
random_seed = 10
 #隨機種子
~~~
創建SOM實例
~~~python
som = MiniSom(som_shape[0], som_shape[1], input_len, sigma=sigma, learning_rate=learning_rate, random_seed=random_seed)
~~~
訓練SOM
~~~python
som.train_random(X, 10000)
 #使用隨機選取的10000個數據點進行訓練
~~~
繪製SOM權重向量
~~~python
plt.figure(figsize=(10, 10))
plt.pcolor(som.distance_map().T, cmap=‘bone_r’)
 # 繪製每個神經元與其鄰居之間距離的地圖
plt.colorbar()
~~~

繪製每個神經元最頻繁地映射到哪個數字類別
~~~python
markers = ['o', 'v', '^', '<', '>', '8', 's', 'p', '*', 'h']
colors = ['C0', 'C1', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7', 'C8', 'C9']

for cnt, xx in enumerate(X):
    w = som.winner(xx)
    # 獲得輸入向量xx對應的贏者神經元
    plt.plot(w[0]+.5, w[1]+.5, markers[y[cnt]], markerfacecolor='None', markeredgecolor=colors[y[cnt]], markersize=12, markeredgewidth=2)
plt.axis([0, som_shape[0], 0, som_shape[1]]) plt.show()
~~~