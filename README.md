# AI-agent-RAG
AI assistant for writing articles with fact-checking in the user's knowledge base.

# n8n RAG Demo — Руководство по запуску

Это руководство описывает шаги, необходимые для локального запуска проекта.

## Шаги для запуска

### 1. Клонировать или сделать fork репозитория

Склонируйте репозиторий на локальную машину:

```bash
git clone <repository_url>
```

Или сделайте **fork** репозитория и затем клонируйте его.

---

### 2. Настроить переменные окружения

Создайте файл в корне проекта .env.
Добавьте необходимые **credentials** и конфигурационные параметры. Пример в файле:

```
.example.env
```

---

### 3. Запустить сервисы через Docker

В корне проекта выполните команду:

```bash
docker compose up -d
```

Это запустит необходимые контейнеры в фоновом режиме.

---

### 4. Импортировать credentials в n8n

После запуска контейнеров выполните команду для импорта workflow из репозитория:

```bash
docker exec -u node -it n8n-rag-demo n8n import:credentials --input=/sync/credentials.json
```

---

### 5. Импортировать workflow в n8n

После запуска контейнеров выполните команду для импорта workflow из репозитория:

```bash
docker exec -it n8n-rag-demo n8n import:workflow --separate --input=/sync/workflows
```

---

### 6. Создать учетную запись в n8n

1. Откройте **n8n** в браузере http://localhost:5678/.
2. Завершите процесс регистрации.
3. Создайте нового пользователя.

---

### 7. Установить ноду (qdrant)

Открыть сценарий 01_RAG_add_files_to_Qdrant, выбрать ноду Upsert Points - нажать install

---

### 8. Заполнить credentials внутри n8n

1. Header Auth Openrouter:
    Name: Authorization
    Value: Bearer {{ $env.OPENROUTER_API_KEY }}

2. QdrantApi account
    API Key: {{ $env.QDRANT_API_KEY }}
    Qdrant URL *: {{ $env.QDRANT_REST_URL }}

3. Qdrant account
    API Key: {{ $env.QDRANT_API_KEY }}
    REST URL *: {{ $env.QDRANT_REST_URL }}

4. OpenRouter account
    API Key *: {{ $env.OPENROUTER_API_KEY }}
 
---

## Примечания

* Workflow-файлы находятся в директории:

```
/sync/workflows
```

* Перед выполнением команд убедитесь, что **Docker запущен**.

