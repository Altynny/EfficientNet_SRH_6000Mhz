# EfficientNet SRH Classifier 6000Mhz

Разметка данных и обучение EfficientNet B0 для классификации радио изображений 6000 МГц.

Все блокноты из [/notebooks](/notebooks/) доступны в Google Colab по ссылкам:
- [example.ipynb](https://colab.research.google.com/drive/1A3vKmqXD0MbfAuSlQQ2mjcy9OvrCN7d9#scrollTo=K7_ER9669NM2)
- [model_training.ipynb](https://colab.research.google.com/drive/1dVyhd9eLFgyG__RA9dsqUw39xCcmKnvF?usp=sharing)
- [ds_prep.ipynb](https://colab.research.google.com/drive/1li5OpToaFn8jtWDMmRy6YYcYjVCAG_Wv)

# Размеченные данные

Датасет был подготовлен с помощью следующего кода [ds_prep.ipynb](/notebooks/ds_prep.ipynb)
в соответствие с классами в [CSV-отчёте](/dataset_6000.csv), полученном после ручной разметки, и заданной структуре:
```
data/
├── train/          # 5,869 изображений (60%)
│   ├── Ok/         # 2,934 изображения
│   └── Bad/        # 2,935 изображений
├── val/            # 1,957 изображений (20%)
│   ├── Ok/         # 978 изображений
│   └── Bad/        # 979 изображений
└── test/           # 1,956 изображений (20%)
    ├── Ok/         # 979 изображений
    └── Bad/        # 977 изображений

```
- Всего - 9782 изображений
  - Bad - 4891
  - Ok - 4891

Google Drive - [data6000.zip (1,03 Гб)](https://drive.google.com/file/d/1RWCqP1Ttm3J-BnQClH9qzdhDSXbAKUwS/view?usp=drive_link)

# Установка
1. Склонируйте содержимое репозитория в нужную вам директорию (например, Effnet)
```bash
git clone https://github.com/Altynny/EfficientNet_SRH_6000Mhz Effnet
```

2. Перейдите в созданную вами директорию
```bash
cd Effnet
```

3. Установите зависимости
```bash
pip install -r requirements.txt 
```

# Использование
!Модель работает исключительно с данными, соответствующими структуре, заданной выше в разделе [Размеченные данные](#размеченные-данные)!

Основные методы класса __EffnetClassifer__: 
- __get_efficientnet_dataloaders__ - подготовка даталоадеров для динамической подгрузки данных
- __load_model__ - загрузка обученной модели из .pth файла
- __save_model__ - сохранение модели
- __train__ - обучение модели
- __evaluate__ - оценка точности модели на тестовых данных
- __confusion_matrix__ - отчёт о точности в виде матрицы ошибок
- __predict__ - классификация изображений моделью

Пример использования модели:
```python
from EffnetClassifier import EffnetClassifier

model = EffnetClassifier(model_name='efficientnet_b0')
model.load_model('models/b0_6000.pth')
model.predict('https://ftp.rao.istp.ac.ru/SRH/SRH0306/cleanMaps/20210712/srh_I_2021-07-12T01:59:42_3100.fit')
```

Также можете опробовать модель в готовом блокноте [example.ipynb](/notebooks/example.ipynb).