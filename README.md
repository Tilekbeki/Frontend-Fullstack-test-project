# Тестовые задания: Frontend и Fullstack

Этот репозиторий связывает два независимых тестовых задания через Git submodules:

| Подмодуль | Репозиторий | Задача | Основной стек |
| --- | --- | --- | --- |
| [`frontend`](./frontend/) | [Frontend-test-project](https://github.com/Tilekbeki/Frontend-test-project) | Dashboard и картотека граждан | React, TypeScript, Ant Design |
| [`fullstack`](./fullstack/) | [Fullstack-test-project](https://github.com/Tilekbeki/Fullstack-test-project) | Dashboard с двумя связанными таблицами и REST API | React, TypeScript, AG Grid, Express, PostgreSQL |

Общие критерии: работоспособность, качество интерфейса и кода, соблюдение требований соответствующего задания. Срок сдачи, указанный в обоих ТЗ, — 1–2 недели. Точный состав и порядок запуска описаны в README каждой папки.

Елизавета подтвердила, что можно самостоятельно выбирать дополнительные библиотеки и инструменты; в частности, допустимы Ant Design, Redux, TypeScript, Express и Docker. В Frontend-задании Express и Docker не используются. В Fullstack-проекте используется `pg-promise` для работы с PostgreSQL.

Исходные тексты заданий находятся отдельно в папке `Downloads` и не входят в проекты. Перед сдачей нужно сверить результат с обоими PDF.

## Структура

```text
frontend-fullstack-test/
├── README.md
├── .gitmodules               # адреса двух отдельных репозиториев
├── package.json              # общие команды и Husky
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

## Клонирование и публикация

```bash
git clone --recurse-submodules https://github.com/Tilekbeki/Frontend-Fullstack-test-project.git
cd Frontend-Fullstack-test-project
```

Если общий репозиторий уже клонирован без подмодулей, выполните `git submodule update --init --recursive`. Обычное обновление `git pull --ff-only && git submodule update --init --recursive` получает именно те версии заданий, которые зафиксированы в общем репозитории.

Каждое задание можно клонировать отдельно. Корень [Frontend-репозитория](https://github.com/Tilekbeki/Frontend-test-project) содержит React-приложение, а корень [Fullstack-репозитория](https://github.com/Tilekbeki/Fullstack-test-project) — `client/`, `server/`, `init-db.sql` и `Readme.md`, как указано в ТЗ.

При изменении задания сначала создайте коммит и выполните `git push` внутри соответствующего подмодуля. Затем в общем репозитории добавьте изменившийся указатель подмодуля в коммит и отправьте его. Иначе новый коммит задания не попадёт в общую сборку.

Файлы `node_modules`, `dist`, `*.tsbuildinfo` и `server/.env` исключены через `.gitignore`; исходники, `package-lock.json`, `.env.example` и скриншоты включены в репозитории.

Во всех трёх npm-пакетах настроены ESLint и Prettier: `npm run lint`, `npm run format:check` и `npm run format`. Правила редактора заданы в `.editorconfig` каждого задания.

## Проверка перед push

Для общего Git-репозитория установите зависимости из его корня:

```bash
npm ci
npm --prefix frontend ci
npm --prefix fullstack/client ci
npm --prefix fullstack/server ci
```

Первый `npm ci` подключает Husky. Перед каждым `git push` из общего репозитория hook запускает форматирование и ESLint для Frontend, Fullstack client и server. Если Prettier изменил отслеживаемые файлы в любом из трёх репозиториев, push прерывается: проверьте результат, создайте коммит и повторите команду. Те же проверки можно запустить вручную через `npm run check:push`.

У каждого подмодуля есть собственный `pre-push` hook: установите зависимости командой `npm ci` в корне подмодуля; для Fullstack дополнительно выполните `npm ci` в `client/` и `server/`.

## Быстрый старт

Для Frontend: `cd frontend && npm ci && npm run dev` — приложение доступно на `http://localhost:5174`.

Для Fullstack: откройте [`fullstack/Readme.md`](./fullstack/Readme.md). Там указаны команды для PostgreSQL, API и React-клиента. Нужны Node.js 20.19+ и Docker с Compose для контейнерного запуска БД. Для Frontend нужны Node.js 22.12+.

## Скриншоты

- Frontend: [обзор](./frontend/screenshots/dashboard.jpg), [картотека](./frontend/screenshots/registry.jpg), [карточка гражданина](./frontend/screenshots/citizen.jpg).
- Fullstack: [обзор](./fullstack/screenshots/overview.jpg), [проекты](./fullstack/screenshots/projects.jpg), [задачи](./fullstack/screenshots/tasks.jpg), [ответственные](./fullstack/screenshots/responsibles.jpg).
