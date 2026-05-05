# Отчёт по лабораторной работе №3

**Тема:** Автоматический деплой сайта с помощью GitHub Actions
**Студент:** Azzi-oo
**Дата:** 2026-05-05

---

## Цель работы
Освоить автоматический деплой статического сайта на GitHub Pages с использованием GitHub Actions.

## Ход работы

### 1. Создание репозитория с локальным контентом
В директории `/Users/azat/Development/laba_3` подготовлены:
- `index.html` — статическая HTML-страница с минимальной разметкой и встроенными стилями;
- `.github/workflows/deploy.yml` — workflow для CI/CD;
- `README.md` — инструкция по проекту.

Инициализация и публикация:
```bash
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/Azzi-oo/github_actions.git
git push -u origin main
```

### 2. Настройка прав Actions
В **Settings → Actions → General → Workflow permissions** включён режим
**Read and write permissions**, чтобы `GITHUB_TOKEN` мог пушить в ветку `gh-pages`.

### 3. Содержимое workflow `.github/workflows/deploy.yml`
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
          publish_branch: gh-pages
```

Шаги:
1. **Checkout** — получение исходников через `actions/checkout@v4`.
2. **Setup Node + build** — оставлены закомментированными (статика без сборки).
3. **Deploy** — публикация содержимого корня в ветку `gh-pages` через `peaceiris/actions-gh-pages@v4`.

Триггеры: пуш в `main` и ручной запуск (`workflow_dispatch`).

### 4. Запуск и публикация
После пуша в `main` workflow запускается автоматически. По завершении создаётся ветка `gh-pages`,
которая указана источником в **Settings → Pages** (Branch: `gh-pages`, папка `/`).

### 5. Проверка
Сайт доступен по адресу:
**https://azzi-oo.github.io/github_actions/**

---

## Ссылки
- Репозиторий: https://github.com/Azzi-oo/github_actions
- Вкладка Actions: https://github.com/Azzi-oo/github_actions/actions
- Опубликованный сайт: https://azzi-oo.github.io/github_actions/

## Скриншоты
> Вставить:
> 1. Скриншот вкладки **Actions** с зелёным статусом workflow `Deploy to GitHub Pages`.
> 2. Скриншот открытого в браузере сайта `https://azzi-oo.github.io/github_actions/`.

## Выводы
В ходе работы освоены:
- структура GitHub Actions workflow (триггеры, jobs, steps);
- использование готовых actions из marketplace (`actions/checkout`, `peaceiris/actions-gh-pages`);
- настройка прав `GITHUB_TOKEN` для пуша в служебную ветку;
- публикация статического сайта на GitHub Pages с автоматическим переразвёртыванием при каждом пуше в `main`.
