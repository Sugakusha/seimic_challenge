# seimic_challenge
segmentation of reflecting horizons


исходные данные данные взяты из соревнования 


|модель|dice|jaccard|эпох|время|
|:------|:-----:|:--------:|:-------:|-------:|
|u-net|0.9953893738843146|0.9910568839737347|107|3ч 45м 8с|
|resnet34-unet|0.9965058061338606|0.9931607264138403|183|6ч 38м 23с|


![наиболее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_resnet.png "ssssss")
![наиболее точное предсказание unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_unet.png)
![наименее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_resnet.png)
![наименее точное предсказание runet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_unet.png)
