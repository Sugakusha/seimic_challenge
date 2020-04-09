# Сегментация сейсмических отражающих горизонтов
## Задача
-Задача: сегментация сейсмических горизонтов в кубе амплитуд мелового и юрского периодов.


-Количество классов: 7

- Количество изображений: 896
  - xline:  512
  - inline:  384
  
- Размеры изображений:
  - xline: 384x512
  - inline:  384х384

## Полезные ссылкы
посты на эту тему:[habr.com](https://habr.com/ru/company/ods/blog/482780/),
[habr.com](https://habr.com/ru/company/ods/blog/488852/)


близкие соревнования:[kaggle.com](https://www.kaggle.com/c/tgs-salt-identification-challenge)


## Данные

исходные данные данные: [booster.ru](https://boosters.pro/championship/rsc_sandbox/overview)



содежимое исходных данных:
+ набор изображений для обучения
+ набор изображений для тестирования
+ baseline на pytorch с ResNet34
+ маски(.csv файл)
+ пример сабмита
+ .npy файлы
+ функции для извлечения изображений из .npy файлов


## Обучение

Для обучения и тестирования исходные изображения были разделены следующим образом: 
+ обучение: 504 изображений
+ валидация: 224 изображений
+ тестирование: 168 изображений

Обучены 2 сети U-net и ResNet34 c общими параметрами:
+ seed: 42
+ epohs: 200 
+ batch: 4
+ loss: 0.75 * (1 - dice) + 0.25 * binary_crossentropy
+ metrics: 1 - dice
+ optimizers: Adam(lr = 0.0001)
+ callbacks: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint

Аугментaция и предобработка изображений:
+ Resize(384, 384)
+ HorizontalFlip(p = 0.5)
+ Rotate(limit = 20, p = 0.5)
+ ElasticTransform(p = 0.5)
+ Normalize(mean = (0.485, 0.456, 0.406), std = (0.229, 0.224, 0.225))



## РЕЗУЛЬТАТЫ

|модель|название файла|dice|jaccard|эпох|время|
|:------|:--------:|:-----:|:--------:|:-------:|-------:|
|u-net|seisma_rosneft_unet.ipynb|0.9953893738843146|0.9910568839737347|107|3ч 45м 8с|
|resnet34|seisma_rosneft_resnet34unet.ipynb|0.9965058061338606|0.9931607264138403|183|6ч 38м 23с|




#### наиболее точное предсказание ResNet34 c jaccard coef = 0.994594 	  dice coef = 0.997265
![наиболее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_resnet.png )
#### наиболее точное предсказание U - Net c jaccard coef = 0.993608 	  dice coef = 0.996741
![наиболее точное предсказание unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/best_dice_unet.png)
#### наименее точное предсказание ResNet34 jaccard coef = 0.990600 	  dice coef = 0.995173
![наименее точное предсказание resnet34+unet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_resnet.png)
#### наименее точное предсказание U - Net c jaccard coef = 0.979881 	   dice coef = 0.989472
![наименее точное предсказание runet](https://raw.githubusercontent.com/Sugakusha/seimic_challenge/master/pic/worst_dice_unet.png)
