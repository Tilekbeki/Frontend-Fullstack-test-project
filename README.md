# Тестовые задания: Frontend и Fullstack

В этой папке находятся два независимых тестовых задания:

| Папка | Задача | Основной стек |
| --- | --- | --- |
| [`frontend`](./frontend/) | Dashboard и картотека граждан | React, TypeScript, Ant Design |
| [`fullstack`](./fullstack/) | Dashboard с двумя связанными таблицами и REST API | React, TypeScript, AG Grid, Express, PostgreSQL |

Общие критерии: работоспособность, качество интерфейса и кода, соблюдение требований соответствующего задания. Срок сдачи, указанный в обоих ТЗ, — 1–2 недели. Точный состав и порядок запуска описаны в README каждой папки.

Елизавета подтвердила, что можно самостоятельно выбирать дополнительные библиотеки и инструменты; в частности, допустимы Ant Design, Redux, TypeScript, Express и Docker. В Frontend-задании Express и Docker не используются. В Fullstack-проекте используется `pg-promise` для работы с PostgreSQL.

Исходные тексты заданий находятся отдельно в папке `Downloads` и не входят в проекты. Перед сдачей нужно сверить результат с обоими PDF.

## Структура

```text
frontend-fullstack-test/
├── README.md
├── package.json              # общие команды и Husky для текущего Git-репозитория
├── .husky/pre-push            # проверка перед push
├── frontend/
│   └── README.md
└── fullstack/
    ├── Readme.md
    ├── client/
    ├── server/
    ├── docker-compose.yml
    └── init-db.sql
```

## Публикация

Сейчас Git и общий `pre-push` hook находятся в `frontend-fullstack-test`: push из этой папки проверяет оба задания. Если сдавать задания строго по структуре ТЗ, создайте **два репозитория**:

1. Репозиторий Frontend: его корень — папка `frontend/`.
2. Репозиторий Fullstack: его корень — папка `fullstack/`, чтобы `client/`, `server/`, `init-db.sql` и `Readme.md` находились в корне репозитория, как указано в ТЗ.

Файлы `node_modules`, `dist`, `*.tsbuildinfo` и `server/.env` исключены через `.gitignore`; исходники, `package-lock.json`, `.env.example` и скриншоты нужно включить в коммит. Ссылки на репозитории добавляются после публикации.

Во всех трёх npm-пакетах настроены ESLint и Prettier: `npm run lint`, `npm run format:check` и `npm run format`. Правила редактора заданы в `.editorconfig` каждого задания.

## Проверка перед push

Для текущего общего Git-репозитория установите зависимости из его корня:

```bash
npm ci
npm --prefix frontend ci
npm --prefix fullstack/client ci
npm --prefix fullstack/server ci
```

Первый `npm ci` подключает Husky. Перед каждым `git push` hook запускает форматирование и ESLint для Frontend, Fullstack client и server. Если Prettier изменил отслеживаемые файлы, push прерывается: проверьте результат, создайте коммит и повторите команду. Те же проверки можно запустить вручную через `npm run check:push`.

В папках `frontend/` и `fullstack/` также лежат собственные hooks для сдачи двумя отдельными репозиториями. После создания каждого Git-репозитория выполните `npm ci` в его корне; для Fullstack дополнительно установите зависимости в `client/` и `server/`.

## Быстрый старт

Для Frontend: `cd frontend && npm ci && npm run dev` — приложение доступно на `http://localhost:5174`.

Для Fullstack: откройте [`fullstack/Readme.md`](./fullstack/Readme.md). Там указаны команды для PostgreSQL, API и React-клиента. Нужны Node.js 20.19+ и Docker с Compose для контейнерного запуска БД. Для Frontend нужны Node.js 22.12+.

## Скриншоты

- Frontend: [обзор](./frontend/screenshots/dashboard.jpg), [картотека](./frontend/screenshots/registry.jpg), [карточка гражданина](./frontend/screenshots/citizen.jpg).
- Fullstack: [обзор](./fullstack/screenshots/overview.jpg), [проекты](./fullstack/screenshots/projects.jpg), [задачи](./fullstack/screenshots/tasks.jpg), [ответственные](./fullstack/screenshots/responsibles.jpg).
