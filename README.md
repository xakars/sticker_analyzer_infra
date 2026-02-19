# Sticker Analyzer Infra

Инфраструктура для анализа стикеров/этикеток. Проект объединяет сервис распознавания текста (OCR) и сервис интеллектуального анализа (LLM) в единый пайплайн.
## Архитектура

Проект построен на микросервисной архитектуре с использованием Docker Compose. Данные между сервисами передаются через общую Docker volume.

- `ocr_padd/gpu-ocr-padd`: Сервис на базе PaddleOCR для извлечения текста из изображений.

- `label_analyzer/`: Сервис для анализа текста с использованием LLM.

Структура проекта:
<img width="1316" height="666" alt="image_2026-02-19_19-59-05" src="https://github.com/user-attachments/assets/ac1db650-3cdc-4554-bf97-e890b5147673" />


## Быстрый старт
### 1. Клонирование репозитория
Так как проект использует git submodules, обычного git clone недостаточно. Используйте:
```bash
git clone --recursive https://github.com/xakars/sticker_analyzer_infra.git
cd sticker_analyzer_infra
```
### 2. Настройка окружения
1) Необходимо создать файл `.env`в директории `./label_analyzer/.env` (см. шаблон `example.env`):

и добавить следующие обязательные данные:

```bash
DEEPSEEK__API_KEY=
OCR_SERVICE_URL=
```
необязательные:
```bash
DEEPSEEK__MAX_CONNECTIONS=
DEEPSEEK__TIMEOUT=
```
где:

- `DEEPSEEK__API_KEY`* - API-ключ аутентификации. [Получить](https://api-docs.deepseek.com/).
- `OCR_SERVICE_URL`=http://ocr_fastapi:8001/ocr/predict-by-folder
- `DEEPSEEK__MAX_CONNECTIONS` - максимальное количество одновременных HTTP-соединений к API
- `DEEPSEEK__TIMEOUT` - лимит времени ожидания ответа от API

2) Необходимо создать файл `.env`в директории `./ocr_padd/.env` (см. шаблон `example.env`):
p.s. временно создаем пустую
```bash

```
### 3. Запуск
Сборка и запуск всех контейнеров одной командой:
```bash
docker-compose up --build
```
API будет доступен по адресу: http://0.0.0.0:8082/api/docs

### Пример работы: 
<img width="1280" height="856" alt="image" src="https://github.com/user-attachments/assets/b078e17f-dcd9-4fe7-8551-404c7f983527" />

