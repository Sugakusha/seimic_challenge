# seimic_challenge
segmentation of reflecting horizons


исходные данные данные взяты из соревнования 


Обучены 2 сети U-net и U-net+ResNet34.
+ seed: 42
+ epohs: 200 
+ batch: 4
+ loss: 0.75 * (1 - dice) + 0.25 * binary_crossentropy
+ optimizers: Adam(lr = 0.0001)
+ callbacks: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint


|модель|dice|jaccard|эпох|время|
|:------|:-----:|:--------:|:-------:|-------:|
|u-net|0.9953893738843146|0.9910568839737347|107|3ч 45м 8с|
|resnet34-unet|0.9965058061338606|0.9931607264138403|183|6ч 38м 23с|

# РЕЗУЛЬТАТЫ


#### наиболее точное предсказание resnet34+unet c jaccard coef = 0.994594 	dice coef = 0.997265
![наиболее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_resnet.png )
#### наиболее точное предсказание resnet34+unet c jaccard coef = 0.993608 	dice coef = 0.996741
![наиболее точное предсказание unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_unet.png)
#### наименее точное предсказание resnet34+unet c jaccard coef = 0.990600 	dice coef = 0.995173
![наименее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_resnet.png)
#### наименее точное предсказание resnet34+unet c jaccard coef = 0.979881 	dice coef = 0.989472
![наименее точное предсказание runet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_unet.png)
