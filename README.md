# Сегментация сейсмических отражающих горизонтов

Задача: сегментация сейсмических горизонтов в кубе амплитуд мелового и юрского периодов.


Количество классов: 7

- Количество изображений: 896
  - инлайнов:  512
  - икслайнов:  384

## Общее
посты на эту тему:[habr.com](https://habr.com/ru/company/ods/blog/482780/),
[habr.com](https://habr.com/ru/company/ods/blog/488852/)


близкие соревнования:[kaggle.com](https://www.kaggle.com/c/tgs-salt-identification-challenge)

исходные данные данные: [booster.ru](https://boosters.pro/championship/rsc_sandbox/overview)



содежимое исходных данных:
+ набор изображений для обучения
+ набор изображений для тестирования
+ baseline на pytorch с U-net+ResNet34
+ маски(.csv файл)
+ пример сабмита
+ .npy файлы
+ функции для извлечения изображений и .npy файлов



Для обучения и тестирования исходные изображения были разделены следующим образом: 
+ обучение: 504 изображений
+ валидация: 224 изображений
+ тестирование: 168 изображений

Обучены 2 сети U-net и U-net+ResNet34 c общими параметрами:
+ seed: 42
+ epohs: 200 
+ batch: 4
+ loss: 0.75 * (1 - dice) + 0.25 * binary_crossentropy
+ optimizers: Adam(lr = 0.0001)
+ callbacks: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint

Аугментaция и предобработка изображений:
+ Resize(384, 384)
+ HorizontalFlip(p = 0.5)
+ Rotate(limit = 20, p = 0.5)
+ ElasticTransform(p = 0.5)
+ Normalize(mean = (0.485, 0.456, 0.406), std = (0.229, 0.224, 0.225))



## РЕЗУЛЬТАТЫ

|модель|dice|jaccard|эпох|время|
|:------|:-----:|:--------:|:-------:|-------:|
|u-net|0.9953893738843146|0.9910568839737347|107|3ч 45м 8с|
|resnet34-unet|0.9965058061338606|0.9931607264138403|183|6ч 38м 23с|




#### наиболее точное предсказание resnet34+unet c jaccard coef = 0.994594 	  dice coef = 0.997265
![наиболее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_resnet.png )
#### наиболее точное предсказание resnet34+unet c jaccard coef = 0.993608 	  dice coef = 0.996741
![наиболее точное предсказание unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_unet.png)
#### наименее точное предсказание resnet34+unet c jaccard coef = 0.990600 	  dice coef = 0.995173
![наименее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_resnet.png)
#### наименее точное предсказание resnet34+unet c jaccard coef = 0.979881 	   dice coef = 0.989472
![наименее точное предсказание runet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_unet.png)
