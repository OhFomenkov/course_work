# Sentinel Monitor (SOC Dashboard)

**Sentinel Monitor** — это система мониторинга утечек учетных данных в реальном времени. Проект предназначен для специалистов по информационной безопасности (SOC-аналитиков) с целью обнаружения скомпрометированных учетных записей сотрудников компании в открытых источниках.

## Основные возможности
- **Telegram Collector**: Автоматический мониторинг Telegram-каналов на наличие "сливов" (email:pass).
- **Web Scraper**: Мониторинг веб-ресурсов (OSINT) для выявления новых дампов.
- **Matching Engine**: Автоматическое сопоставление утекших данных с реестром сотрудников.
- **SOC Dashboard**: Веб-интерфейс на Flask для управления инцидентами, источниками и анализа безопасности.

## Технологический стек
- **Язык**: Python 3.10+
- **Backend**: Flask
- **База данных**: PostgreSQL
- **Парсинг**: Telethon (Telegram API), BeautifulSoup4, Requests
- **UI**: Bootstrap 5, Jinja2

## Быстрый запуск

### 1. Подготовка
```bash
# Клонирование репозитория
git clone https://github.com/ВАШ_ЛОГИН/leak-monitor.git
cd leak-monitor

# Создание виртуального окружения
python -m venv venv
venv\Scripts\activate  # Для Windows

# Установка зависимостей
pip install -r requirements.txt
2. Конфигурация
Создайте файл .env в корне проекта на основе .env.example и укажите необходимые данные:
Данные для подключения к PostgreSQL (DB_NAME, DB_USER, DB_PASSWORD, и т.д.)
Telegram API Credentials (API_ID, API_HASH, BOT_TOKEN)
Секретный ключ (SECRET_KEY) - для подписи сессии(Cookies)
Для генерации секретного ключа используйте:
python -c "import secrets; print(secrets.token_hex(32))"
3. Инициализация базы данных
code
Bash
# Создание таблиц
python -m app.database.db_init

# Наполнение демо-данными для проверки
python scripts/db_seed.py
4. Запуск
code
Bash
# Запуск веб-интерфейса
python run.py --mode=web

# В отдельном терминале (для парсинга Telegram)
python run.py --mode=bot
Демонстрация
Для тестирования парсера без выхода в реальные сети:
Запустите имитатор форума: python dev_tools/forum_mock.py
Укажите http://127.0.0.1:5001 в качестве TARGET_URL в файле .env.
Нажмите "Запустить сканер" в разделе веб-скрапера на дашборде.
