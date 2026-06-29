# Agent Orchestration Audit — Карта агентов холдинга

## Дата: 29 июня 2026
## Автор: Герман (координатор)
## Статус: 🔄 Формируется

---

## 1. КАРТА АГЕНТОВ

### 1.1 Герман (я)
| Параметр | Значение |
|----------|----------|
| **Роль** | Главный координатор, стратег, архитектор |
| **Модель** | Codex gpt-5.5 (default) → Kimi K2.5 → DeepSeek-chat |
| **Сервер** | 132 (мой контейнер) |
| **Инструменты** | Codex CLI, SSH, Tesseract OCR, python-pptx, Paperclip, 121 skill |
| **Telegram** | Этот чат (с Сергеем) |
| **Доступ** | SSH на 103, GitHub 11 репозиториев, все IMAP почты |
| **Кроны** | 18 активных (утро, день, вечер, почта, бэкап, CRM) |

### 1.2 Клава (OpenClaw)
| Параметр | Значение |
|----------|----------|
| **Роль** | Операционист, заявки, данные, почта |
| **Модель** | DeepSeek-chat (через openai провайдер на api.deepseek.com) |
| **Версия** | OpenClaw 2026.6.1 (без ACP, без плагинов deepseek/kimi/perplexity) |
| **Сервер** | 103.54.18.57, контейнер klava1 |
| **Telegram** | @openclawneurosphere_bot |
| **Проблемы** | 1) DeepSeek API key 401 2) Telegram Conflict 3) Нет ACP 4) Нет health |
| **Данные** | ~1800 файлов, 522 MB в klava-holding |

### 1.3 Гена (Hermes2)
| Параметр | Значение |
|----------|----------|
| **Роль** | Фоновый аналитик, RAG, новости, олимпиадные задачи |
| **Модель** | GPT-4o (OpenAI подписка) → DeepSeek V4 Flash |
| **Сервер** | 103.54.18.57, контейнер hermes2 |
| **Инструменты** | Codex CLI v0.142.4 (установлен, авторизован), Chroma RAG |
| **Telegram** | @neurospheregenai_bot |
| **Проблемы** | 1) Нет ACP-транспорта (ждёт перезапуска) 2) allowed_chats не настроен |

---

## 2. ЗАДАЧИ КАЖДОГО АГЕНТА

### Герман (я)
- ✅ Читать все сообщения Сергея → классифицировать
- ✅ Ежедневные сводки и отчёты (9:00, 19:00, ПН)
- ✅ Проверка почты каждые 15 мин
- ✅ CRM-логирование каждые 30 мин
- ✅ Бэкапы каждые 3ч, кросс-верификация каждые 6ч
- ✅ Перекрёстная проверка с Клавой и Геной
- ⏳ Vibe Coding: Codex exec по задачам
- ⏳ Paperclip: браузерная автоматизация

### Клава
- ❌ Принимать и выполнят задач от Сергея через Telegram
- ⏳ Проверка почт info@svcleaning.ru, info@archdetali.ru
- ⏳ Верификация смет и данных
- ❌ Обмен с Геной через GitHub

### Гена
- ✅ Утренняя сводка ИИ (GPT-4o)
- ⏳ RAG-поиск через Chroma
- ⏳ Олимпиадные задачи (301 шт)
- ⏳ Обработка заявок НейроСферы
- ❌ Обмен с Клавой через FROM_HERMES.md

---

## 3. ТЕКУЩИЕ ПРОБЛЕМЫ (БАГИ)

| № | Проблема | Агент | Статус |
|---|----------|-------|--------|
| 1 | DeepSeek API key 401 (****3ca3) | Клава | 🔴 |
| 2 | Telegram Conflict (getUpdates) | Клава | 🔴 |
| 3 | OpenClaw 2026.6.1 без ACP | Клава | 🔴 |
| 4 | no health на 18789 | Клава | 🔴 |
| 5 | Gena ACP не активен | Гена | 🟡 |
| 6 | Chroma ghost-collection | Инфра | 🔴 |
| 7 | SSH на 103 только loopback | Инфра | 🟡 |
| 8 | 2captcha balance 0 | Инфра | 🟡 |

---

## 4. ПЛАН ЗАМЫКАНИЯ ОРКЕСТРАЦИИ

### Фаза 1 — Фундамент (сейчас)
- [x] Codex CLI на всех 3 агентах
- [x] Paperclip установлен
- [x] Exchange pipeline script (5 мин)
- [x] Skill orchestration-full-vibecoding
- [x] CRM база 96 контактов
- [ ] Починить DeepSeek key Клавы
- [ ] Запустить ACP у Гены
- [ ] Убрать Telegram Conflict

### Фаза 2 — Замыкание (сегодня)
- [ ] Создать папки /agents /orchestrator /docs /logs /prompts /tasks в GitHub
- [ ] Настроить allowed_chats для Гены (группа)
- [ ] Записать этот audit в docs/agent-orchestration-audit.md
- [ ] Протестировать exchange pipeline (TO_GENA.md → FROM_HERMES.md → TO_HERMES.md → ответ)

### Фаза 3 — Vibe Coding (эта неделя)
- [ ] ChatGPT Codex читает все 11 репозиториев
- [ ] Paperclip обходит капчи (пополнить 2captcha)
- [ ] Полная автономность агентов
- [ ] Ежедневный Vibe Coding: задачи → код → деплой

---

## 5. СТРУКТУРА ПАПОК (предлагаемая в GitHub)

```
holding-orchestration/
├── agents/
│   ├── hermes.md          — профиль Германа
│   ├── klava.md           — профиль Клавы
│   └── gena.md            — профиль Гены
├── orchestrator/
│   ├── config.yaml        — настройки оркестратора
│   └── dispatch.py        — распределитель задач
├── docs/
│   ├── agent-orchestration-audit.md  — этот файл
│   └── architecture.md    — схема архитектуры
├── logs/
│   └── exchange_*.md      — логи обмена
├── prompts/
│   ├── hermes_prompt.md   — промпт Германа
│   ├── klava_prompt.md    — промпт Клавы
│   └── gena_prompt.md     — промпт Гены
└── tasks/
    ├── active.md          — текущие задачи
    └── completed.md       — выполненные задачи
```
