# Airbnb MLOps

Курсовой проект ML/DLOps (НИУ ВШЭ, магистратура «Аналитика больших данных», 2026).

## Задача

Регрессия: предсказать цену за ночь (`price`) объявления Airbnb в Лондоне по его характеристикам: расположению, вместимости, числу спален и ванных, типу жилья и району.

## Данные

[Inside Airbnb](https://insideairbnb.com/), подготовленный снимок Лондона от 2026-03-21: 5724 объявления, 13 колонок.

| Группа | Колонки |
|---|---|
| Числовые признаки | `latitude`, `longitude`, `accommodates`, `bathrooms`, `bedrooms`, `beds`, `minimum_nights` |
| Категориальные признаки | `neighbourhood_cleansed` (33 района), `property_type` (51 тип), `room_type` (4 типа) |
| Целевая переменная | `price` |
| Служебные (не используются как признаки) | `listing_id`, `snapshot_date` |

Данные лежат в S3-совместимом хранилище Yandex Object Storage и читаются напрямую через `boto3`. Скачивать файл вручную не нужно.

## Структура проекта

```
airbnb-mlops/
├── notebooks/
│   └── 01_read_data.ipynb   # семинар 1: чтение CSV из S3 с локальной копией
├── src/                     # Python-скрипты (обучение, API)
├── docker/                  # Dockerfile для обучения и API
├── .env.example             # шаблон переменных окружения
├── requirements.txt         # зависимости
└── README.md
```

Каталоги `data/` (локальная копия CSV) и `models/` (`model.pkl`) создаются при запуске и в git не хранятся.

## Настройка S3

Ключи доступа передаются только через переменные окружения и в репозиторий не попадают.

| Переменная | Описание | Пример |
|---|---|---|
| `AWS_ACCESS_KEY_ID` | ID ключа доступа | выдаёт преподаватель |
| `AWS_SECRET_ACCESS_KEY` | секретный ключ | выдаёт преподаватель |
| `AWS_DEFAULT_REGION` | регион | `ru-central1` |
| `S3_ENDPOINT_URL` | endpoint хранилища | `https://storage.yandexcloud.net` |
| `S3_BUCKET` | bucket | `mlops26-course-bucket` |
| `S3_KEY` | ключ объекта | `prepared/train.csv` |

Проще всего скопировать шаблон и вписать ключи:

```bash
cp .env.example .env    # Windows: copy .env.example .env
```

Ноутбуки подхватывают `.env` автоматически через `python-dotenv`.

## Запуск

Окружение (Python 3.11+):

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Ноутбуки открываются в VS Code с расширением Jupyter (или `jupyter lab`), ячейки выполняются сверху вниз.

## Работа с репозиторием

Каждая часть задания делается в отдельной ветке от актуального `main` (`feature/...`) и вливается через Pull Request.
