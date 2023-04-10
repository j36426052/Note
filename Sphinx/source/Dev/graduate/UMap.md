# UMamp.md

## Introduction

目前在我們的機器學習中有個lantent space，但概念十分的抽象，因此要用UMap把它給畫出來，目前有以下幾片要參考

1. [抓取lantent space的向量](https://www.tensorflow.org/tutorials/generative/cvae)
2. [基礎使用Umap](https://umap-learn.readthedocs.io/en/latest/basic_usage.html)
3. [進階，用umap導入新數據](https://umap-learn.readthedocs.io/en/latest/transform.html)

ideas of latent space [IDEA](https://towardsdatascience.com/understanding-latent-space-in-machine-learning-de5a7c687d8d)

## Autoencoder

[介紹](https://medium.com/ml-note/autoencoder-%E4%B8%80-%E8%AA%8D%E8%AD%98%E8%88%87%E7%90%86%E8%A7%A3-725854ab25e8)

## 實作
目前看起來最實用：[Median](https://medium.com/mlearning-ai/latent-space-representation-a-hands-on-tutorial-on-autoencoders-in-tensorflow-57735a1c0f3f)

目前先將最後一層的參數叫出來：
[參考的程式碼](https://keras.io/getting_started/faq/#how-can-i-obtain-the-output-of-an-intermediate-layer-feature-extraction)
[網友支援如何命名](https://stackoverflow.com/questions/43871162/how-to-get-output-of-hidden-layer-given-an-input-weights-and-biases-of-the-hidd)

~~~py
model = keras.models.load_model('model')

scores = model.evaluate(x_Test_norm, y_TestOneHot)

layer_name = 'last'
sample = x_Test_norm
intermediate_layer_model = keras.Model(inputs=model.input,outputs=model.get_layer(layer_name).output)
intermediate_output = intermediate_layer_model(sample)

print(type(intermediate_output))        #<class 'tensorflow.python.framework.ops.EagerTensor'>
print(len(intermediate_output))         #輸出：sample的數量
print(type(intermediate_output[100]))   #<class 'tensorflow.python.framework.ops.EagerTensor'>
print(len(intermediate_output[100]))    #輸出：最後一層unit的數量
~~~


