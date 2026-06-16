# Тест задание от ООО Литий СБ: Telegram-бот ZIBELINO

Коммерческий Telegram-бот для бренда аксессуаров ZIBELINO. Бот знакомит пользователя с брендом через короткие визуальные карточки, отправляет ссылки на маркетплейсы, показывает актуальные акции, ведет в соцсети и помогает выбрать устройство, чтобы сформировать персональные поисковые ссылки на маркетплейсы.

## Технологический стек

- Python 3.12+
- aiogram 3.x
- python-dotenv
- pytest для простых unit-тестов

**По техническим требованиям, в проекте не используются база данных, Redis, webhooks, Docker, внешние API или интеграции с API маркетплейсов.**

## Установка

```bash
cd project
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Конфигурация

Создайте `.env` на основе примера:

```bash
cp .env.example .env
```

Пример `.env`:

```env
BOT_TOKEN=1234567890:replace_with_your_telegram_bot_token
MEDIA_DIR=media
```

Поместите изображения брендовых карточек в папку `media/`:

- `media/start.jpg` — приветственная карточка бренда
- `media/shops.jpg` — карточка каталога и маркетплейсов
- `media/promo.jpg` — карточка с акциями
- `media/socials.jpg` — карточка соцсетей

Если изображение отсутствует, бот не падает: он отправит текст и кнопки без картинки.

## Запуск

```bash
python bot.py
```

Бот работает только в режиме polling.

## Тесты

```bash
pytest
```

## Структура проекта

```text
project/
├── bot.py
├── config.py
├── handlers.py
├── texts.py
├── keyboards.py
├── devices.py
├── services/
│   └── marketplace.py
├── media/
│   ├── start.jpg
│   ├── shops.jpg
│   ├── promo.jpg
│   └── socials.jpg
├── tests/
│   └── test_marketplace.py
├── .env.example
├── requirements.txt
└── README.md
```

## Примечания

- Выбор устройства реализован через FSM-состояния aiogram: `choosing_brand`, `choosing_model`, `device_selected`.
- Данные выбранного устройства хранятся в памяти FSM в формате `{"brand": "...", "model": "..."}`.
- Ссылки на маркетплейсы генерируются локально с помощью `urllib.parse.quote_plus`.
- Неподдерживаемый пользовательский текст возвращает пользователя в главное меню.
- Навигация по меню поддерживает чат чистым: предыдущий экран бота удаляется после отправки нового.
