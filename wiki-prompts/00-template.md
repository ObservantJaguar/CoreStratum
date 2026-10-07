# Инструкция для ИИ-ассистента: построение self-hosted wiki на GitHub Pages

> **Как использовать:** скопируйте этот файл целиком в новое окно/чат MultiTool и следуйте указаниям. Эта инструкция одиночная — она задаёт общий процесс. Чтобы получить wiki по конкретной теме, объедините этот шаблон с тематической инструкцией (01-криптовалюты, 02-нейросети, 03-дистрибутивы).

## Что вы должны построить

Статическую wiki-энциклопедию на английском языке, собираемую Jekyll + Just the Docs, публикуемую на GitHub Pages. Структура — три класса: **Theory** (теория/концепции), **Tools** (энциклопедия ПО или тематических инструментов), **Practice** (практические руководства).

## Ключевые архитектурные решения (проверены на практике)

### Структура репозитория

```
<repo>/
├── docs/                      <- GitHub Pages source (НЕ корень!)
│   ├── _config.yml            <- конфиг для Pages (remote_theme)
│   ├── _config_local.yml      <- локальный конфиг (theme)
│   ├── Gemfile, Gemfile.lock  <- для локальной сборки
│   ├── index.md               <- главная (title + layout: home + permalink: /)
│   ├── sections/
│   │   ├── theory.md          <- секция Theory (has_children: true)
│   │   ├── tools.md           <- секция Tools
│   │   └── practice.md        <- секция Practice
│   ├── <domain-1>/
│   │   ├── index.md           <- домен (parent: <Секция>, has_children: true)
│   │   └── <category>/index.md <- категория (parent: <Домен>, grand_parent: <Секция>)
│   └── guides/                <- практические руководства (или свои)
├── README.md
└── .gitignore
```

**Критично:** GitHub Pages настроен на ветку `main` + папку `/docs`. Поэтому конфиг Jekyll обязан лежать в `docs/`, а не в корне репозитория.

### Навигация Just the Docs (трёхуровневая)

| Уровень | Front matter |
|---|---|
| Секция (Theory/Tools/Practice) | `title: Theory`, `nav_order: 1`, `has_children: true` |
| Домен (родитель = секция) | `parent: <Секция>`, `title: <Домен>`, `nav_order: N`, `has_children: true` |
| Категория (родитель = домен) | `parent: <Домен>`, `grand_parent: <Секция>`, `title: <Категория>` |
| Программа/страница (родитель = категория) | `parent: <Категория>`, `title: <Имя>` |

Именно так Just the Docs строит выпадающее меню. Если у категории есть `parent` — всегда добавляйте и `grand_parent` (иначе она не отобразится под доменом).

### Конфигурация Jekyll

**`docs/_config.yml`** (для GitHub Pages):

```yaml
remote_theme: just-the-docs/just-the-docs@v0.8.2
title: <Название>
description: <Описание>
url: "https://<USER>.github.io"
baseurl: "/<REPO-NAME>"
permalink: pretty
color_scheme: light
nav_sort: case_insensitive
back_to_top: true
last_edit_timestamp: true

defaults:
  - scope:
      path: ""
    values:
      layout: "default"

just_the_docs:
  navigation_depth: 4

plugins:
  - jekyll-remote-theme
  - jekyll-seo-tag
  - jekyll-sitemap
  - jekyll-relative-links
```

**`docs/_config_local.yml`** (для локального просмотра):

```yaml
theme: just-the-docs
plugins:
  - jekyll-seo-tag
  - jekyll-sitemap
  - jekyll-relative-links

defaults:
  - scope:
      path: ""
    values:
      layout: "default"
```

Локальный сервер запускается так:

```bash
bundle exec jekyll serve --source docs --destination docs/_site --config docs/_config.yml,docs/_config_local.yml
```

URL: `http://127.0.0.1:4000/<REPO-NAME>/`

### ⚠️ Кодировка файлов — самое важное правило

**Никогда не используйте `Get-Content`/`Set-Content` на Windows (PowerShell 5.1) без явной кодировки** — это читает/пишет в Windows-1251 и ломает UTF-8 (тире `—`, стрелки `→`, символы рамок диаграмм превращаются в мусор «РІвЂќ»).

**Правило записи всех .md-файлов:**

```powershell
[System.IO.File]::WriteAllText($path, $text, (New-Object System.Text.UTF8Encoding($false)))
```

**И «чтения»:**
```powershell
$text = [System.Text.Encoding]::UTF8.GetString([System.IO.File]::ReadAllBytes($path))
```

- Никаких кириллических строк внутри PowerShell-команд (ломается парсер).
- Для массовых правок front matter (например, переименовать домен) используйте байтовые замены или Write-инструмент, а не `-replace` через Get-Content.
- Результат всегда проверяйте: `[regex]::Matches($text, '[\u0400-\u04FF]{2,}')` должно быть 0 (если контент не содержит легитимной кириллицы).
- В ASCII-диаграммах (код-блоки) используйте только символы `+ - | * /`, а не box-drawing (`─│┌└`) — они рискованны при чтении через консоль.

## Стандартный рабочий процесс

1. **Создайте репозиторий** на GitHub (например `<REPO-NAME>`), в настройках включите Pages: ветка `main`, папка `/docs`.
2. **Инициализируйте структуру**: папки доменов по TOC, секции, index.md.
3. **Настройте `docs/_config.yml`** по шаблону выше.
4. **Наполняйте контент** по тематической инструкции.
5. **Проверяйте локально**: `bundle exec jekyll build --source docs --destination docs/_site --config docs/_config.yml,docs/_config_local.yml` + запросы к `http://127.0.0.1:4000/...`.
6. **Проверяйте целостность** (обязательный чек-лист перед push):
   - Все относительные .md-ссылки существуют (прогнать сканер).
   - Каждый `parent:` в front matter имеет страницу с таким `title:`.
   - Всё в UTF-8, нет битых фрагментов (см. правило выше).
   - `bundle exec jekyll build` завершается без ошибок; сайт рендерится с темой (ищите `site-nav` и `just-the-docs` в HTML).
7. **Git-команды** (git для Windows уже установлен):
   ```bash
   git config user.name "Observant Jaguar"
   git config user.email "m.a.okopny@gmail.com"
   git add -A
   git commit -m "msg"
   git push origin main
   ```

## Итоговая проверка на GitHub Pages

- После push GitHub Pages пересоберёт сайт (1–3 минуты). URL: `https://<USER>.github.io/<REPO-NAME>/`.
- Проверьте: главная рендерится с темой, навигация раскрывается (секции → домены → категории), ни одна страница не отдаёт 404.
- Проверьте отсутствие битой кодировки на HTML-странице (поиск `�` или кириллических «РІ» в английском контенте).