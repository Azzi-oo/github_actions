# Лабораторная работа №3 — Автодеплой через GitHub Actions

## Цель
Освоить автоматический деплой статического сайта на GitHub Pages с помощью GitHub Actions.

## Шаги выполнения

### 1. Создание репозитория
```bash
git init
git add .
git commit -m "Initial commit: static site + deploy workflow"
git branch -M main
git remote add origin https://github.com/<ваш_логин>/<имя_репозитория>.git
git push -u origin main
```

### 2. Настройка прав Actions
В настройках репозитория: **Settings → Actions → General → Workflow permissions** —
выбрать **Read and write permissions**, сохранить.

### 3. Workflow
Файл `.github/workflows/deploy.yml` выполняет:
- `checkout` исходного кода;
- (опционально) установку Node.js и сборку — закомментировано;
- деплой через `peaceiris/actions-gh-pages@v4` в ветку `gh-pages`.

### 4. Включение GitHub Pages
После первого успешного запуска workflow появится ветка `gh-pages`.
В **Settings → Pages** указать: **Source = Deploy from a branch**, **Branch = gh-pages**, папка `/`.

### 5. Проверка
Сайт будет доступен по адресу:
```
https://<ваш_логин>.github.io/<имя_репозитория>/
```

## Структура проекта
```
.
├── .github/workflows/deploy.yml   # CI/CD pipeline
├── index.html                     # Статический контент
└── README.md
```
