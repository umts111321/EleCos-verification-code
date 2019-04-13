# EleCos-confirmation-code

## Selenium
  Download [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads)


## Confirmation code

6 strings can be seen in [Handler1.ashx](https://www.ais.tku.edu.tw/EleCos/Handler1.ashx), they are confirmation code answers.

```python
code = {'b6589fc6ab0dc82cf12099d1c2d40ab994e8410c': '0',
        '356a192b7913b04c54574d18c28d46e6395428ab': '1',
        'da4b9237bacccdf19c0760cab7aec4a8359010b0': '2',
        '77de68daecd823babbb58edb1c8e14d7106e83bb': '3',
        '1b6453892473a467d07372d45eb05abc2031647a': '4',
        'ac3478d69a3c81fa62e60f5c3696165a4e5e6ac4': '5',
        'c1dfd96eea8cc2b62785275bca38ac261256e278': '6',
        '902ba3cda1883801594b6e1b452790cc53948fda': '7',
        'fe5dbbcea5ce7e2988b8c69bcfdfde8904aabc1f': '8',
        '0ade7c2cf97f75d009975f4d720d1fa6c19f4897': '9'}
```

## Get IMG and PP
```
> python "get_IMG&PP.py"
```

### Get IMG
We need train(60k), valid(15k), test(20k).

### PP
Keep only yellow.

## Training
```
> python train.py
```

### model.summary()
```
__________________________________________________________________________________________________
Layer (type)                    Output Shape         Param #     Connected to                     
==================================================================================================
input_1 (InputLayer)            (None, 32, 120, 3)   0                                            
__________________________________________________________________________________________________
conv2d_1 (Conv2D)               (None, 32, 120, 32)  896         input_1[0][0]                    
__________________________________________________________________________________________________
conv2d_2 (Conv2D)               (None, 30, 118, 32)  9248        conv2d_1[0][0]                   
__________________________________________________________________________________________________
batch_normalization_1 (BatchNor (None, 30, 118, 32)  128         conv2d_2[0][0]                   
__________________________________________________________________________________________________
max_pooling2d_1 (MaxPooling2D)  (None, 15, 59, 32)   0           batch_normalization_1[0][0]      
__________________________________________________________________________________________________
conv2d_3 (Conv2D)               (None, 15, 59, 64)   18496       max_pooling2d_1[0][0]            
__________________________________________________________________________________________________
conv2d_4 (Conv2D)               (None, 13, 57, 64)   36928       conv2d_3[0][0]                   
__________________________________________________________________________________________________
batch_normalization_2 (BatchNor (None, 13, 57, 64)   256         conv2d_4[0][0]                   
__________________________________________________________________________________________________
max_pooling2d_2 (MaxPooling2D)  (None, 6, 28, 64)    0           batch_normalization_2[0][0]      
__________________________________________________________________________________________________
conv2d_5 (Conv2D)               (None, 6, 28, 128)   73856       max_pooling2d_2[0][0]            
__________________________________________________________________________________________________
conv2d_6 (Conv2D)               (None, 4, 26, 128)   147584      conv2d_5[0][0]                   
__________________________________________________________________________________________________
batch_normalization_3 (BatchNor (None, 4, 26, 128)   512         conv2d_6[0][0]                   
__________________________________________________________________________________________________
max_pooling2d_3 (MaxPooling2D)  (None, 2, 13, 128)   0           batch_normalization_3[0][0]      
__________________________________________________________________________________________________
conv2d_7 (Conv2D)               (None, 2, 13, 256)   295168      max_pooling2d_3[0][0]            
__________________________________________________________________________________________________
conv2d_8 (Conv2D)               (None, 2, 13, 256)   590080      conv2d_7[0][0]                   
__________________________________________________________________________________________________
batch_normalization_4 (BatchNor (None, 2, 13, 256)   1024        conv2d_8[0][0]                   
__________________________________________________________________________________________________
max_pooling2d_4 (MaxPooling2D)  (None, 1, 6, 256)    0           batch_normalization_4[0][0]      
__________________________________________________________________________________________________
flatten_1 (Flatten)             (None, 1536)         0           max_pooling2d_4[0][0]            
__________________________________________________________________________________________________
dropout_1 (Dropout)             (None, 1536)         0           flatten_1[0][0]                  
__________________________________________________________________________________________________
digit1 (Dense)                  (None, 10)           15370       dropout_1[0][0]                  
__________________________________________________________________________________________________
digit2 (Dense)                  (None, 10)           15370       dropout_1[0][0]                  
__________________________________________________________________________________________________
digit3 (Dense)                  (None, 10)           15370       dropout_1[0][0]                  
__________________________________________________________________________________________________
digit4 (Dense)                  (None, 10)           15370       dropout_1[0][0]                  
__________________________________________________________________________________________________
digit5 (Dense)                  (None, 10)           15370       dropout_1[0][0]                  
__________________________________________________________________________________________________
digit6 (Dense)                  (None, 10)           15370       dropout_1[0][0]                  
==================================================================================================
Total params: 1,266,396
Trainable params: 1,265,436
Non-trainable params: 960
__________________________________________________________________________________________________
```

- patience = 5
- batch_size = 400
- epochs = 100

## Test
```
> python test.py
```

Correct rate: 0.99955