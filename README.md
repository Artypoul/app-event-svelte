![Svelte Logo](https://st.timeweb.com/cloud-static/apps-logo/svelte.svg)

# app-event-svelte

Стартовый репозиторий для Svelte-приложения, подготовленный для локальной разработки и деплоя в Timeweb Cloud Apps.

:tada: [Демо](https://timeweb-cloud-app-example-svelte-b1bc.twc1.net)

:rocket: [Создать свой Apps](https://timeweb.cloud/my/apps/create)

:books: [Документация Timeweb Cloud Apps](https://timeweb.cloud/docs/apps)

## Требования

- Node.js 18+
- npm 9+

## Локальный запуск

```bash
# установка зависимостей
npm install

# режим разработки (watch + автообновление)
npm run dev

# запуск статического сервера для собранного приложения
npm run start
```

## Скрипты

- `npm run dev` — rollup в watch-режиме.
- `npm run build` — production-сборка в `public/build`.
- `npm run start` — запуск `sirv` для директории `public`.
- `npm run preview` — сборка и сразу запуск локального сервера.
- `npm run check` — базовая проверка через production-сборку.

## Рекомендации по работе

1. Хранить компоненты в `src/` с явным разделением на UI- и feature-уровни.
2. Перед каждым коммитом запускать `npm run check`.
3. Использовать единый стиль форматирования через `.editorconfig`.
