# Kryptonite ML Challenge – Команда MMG

## Оглавление

1. [Шапка](#демо)
    - [Демо](#демо)
    - [Описание задачи](#описание-задачи)
    - [Ссылки](#ссылки)
    - [Технологический стек](#технологический-стек)
    <!-- - [Состав команды]() -->
2. [Установка и запуск](#клонирование)
    - [Клонирование](#клонирование)
    - [Запуск в контейнере](#запуск-в-контейнере)
    - [Запуск в локальной среде](запуск-в-локальной-среде)
    - [Инференс](#инференс)
    - [Обучение](#обучение)
    - [Конвертация в onnx](#конвертация-в-onnx)
3. [Структура проекта](#структура-проекта)
    - [Масштабирование](#планы-масштабирования-системы)

## Демо
<видео-gif тут>

## Описание задачи
Поддельные изображения и видео, созданные с помощью технологии DeepFake, представляют угрозу для цифровой безопасности. Они могут быть настолько реалистичными, что их сложно отличить от настоящих.

Предстоит создать модель распознавания лиц, которая должна уметь:

* сравнивать реальные фотографии одного и того же человекаразличать снимки разных людейраспознавать фальшивые изображения, созданные с помощью DeepFake-технологий, без использования модулей защиты от спуфинга
* сравнивать реальные фотографии одного и того же человека
* различать снимки разных людей

## Ссылки
Лендинг: [kryptonite-ml.ru](https://kryptonite-ml.ru) \
Репозиторий: [git.codenrock.com/kryptonite-ml-challenge-1347](https://git.codenrock.com/kryptonite-ml-challenge-1347) \
Тестирующая система: [codenrock.com/contests/kryptonite-ml-challenge](https://codenrock.com/contests/kryptonite-ml-challenge/)

<!-- ## Состав команды
* **Денис Маликов** – DA
* **Артём Таратин** – Капитан, DS
* **Даниил Аль-Натор** – DS
* **Илья Обухов** – DE -->

## Технологический стек
- **Система** Ubuntu 22.04
- **Язык:** Python 3.12+
- **Фреймворк глубокого обучения:** PyTorch
- **Экспорт модели:** ONNX
- **Инференс:** ONNX Runtime
- **Выравнивание лиц:** Пользовательский модуль
- **Обработка данных:** PIL, NumPy, torchvision
- **CLI и утилиты:** argparse, tqdm

## Клонирование
```nushell
git clone https://github.com/kekwak/Kryptonite-ML-Challenge.git
cd Kryptonite-ML-Challenge
```

## Запуск в контейнере
Собрать контейнер самому:
```nushell
...
```
или скачать готовый образ:
```nushell
...
```
а также запуск через альтернативный докерфайл:
```nushell
...
```

## Запуск в локальной среде
В проекте исспользуется анаконда.
* При установке зависимостей этим способом могут возникнуть проблемы.

```nushell
conda env create -f environment.yml && conda activate krypto
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126 --force-reinstall
pip3 install numpy==2.2.3
```

## Инференс

Для начала нужно скачать обученную модель с гугл диска. Это можно сделать вручную или испольовать скрипт для загрузки моделей без аргумента `--all`:
```nushell
python3 models/download_pretrained_models.py
```

Публичный или приватный датасет нужно разместить в папке data, вот таким образом:
```nushell
data
└── test_public
   └── images
        ├── 00000000
        │   ├── 0.jpg
        │   └── 1.jpg
        ├── 00000001
        │   ├── 0.jpg
        │   └── 1.jpg
        ├── ...
        ...
...
```

Как только предыдущие шаги будут выполнены, можно приступать к инференсу. Он запускается вот такой вот командой:
```nushell
python3 scripts/inference.py --model models/onnx/ckpt_epoch1_batch20_acc0.9597_eer0.0282.onnx
```
В аргументах достаточно указать только модель, но и есть возможность указать другую папку с изображениями при помощи аргумента `--test_dir data/path/to/images`

## Обучение

Перед началом обучения нужно скачать все предобученные модели с гугл диска. Это можно сделать вручную или испольовать скрипт для загрузки моделей с аргументом `--all`:
```nushell
python3 models/download_pretrained_models.py --all
```
Уже скачанные модели перезапишутся.

...

## Конвертация в onnx

Для конвертации обученной модели в onnx формат, достаточно использовать команду:
```nushell
python3 scripts/convert.py --checkpoint path/to/model.ckpt --output_model path/to/onnx_model.onnx
```

## Структура проекта
```nushell
.
├── app
│   ├── __init__.py
...
```

## Планы масштабирования системы
- Можно обучать модели верификации не только на диффузионных моделях, но и на задачу Face Swap, используя GAN и те же диффузионные модели
- ...
