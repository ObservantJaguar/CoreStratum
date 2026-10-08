# Тематическая инструкция: wiki «Zelirion» — каталог дистрибутивов и сборка ISO

> **Как использовать:** объедините с общим шаблоном `00-template.md` — сначала вставьте шаблон (структура репозитория, конфиги Jekyll, правила кодировки, работа с Git), затем эту тематическую часть. Скопируйте весь текст в новый чат MultiTool.

## Что это за проект

**Zelirion** — это семейство дистрибутивов (meta-distribution): единая архитектура сборки, которая генерирует ISO-образы с разными Desktop Environment (DE) на разных платформах:

- **Linux (Devuan)** — классическая UNIX-архитектура без systemd (elogind, eudev, sysvinit/OpenRC/runit), полный X11, частичный Wayland.
- **FreeBSD** — полный X11, частичный Wayland.
- **illumos (OpenIndiana / OmniOS)** — Solaris-подобная UNIX, полный X11, без Wayland.

Поддерживаемые DE: Xfce, Cinnamon, Deepin, LXQt, MATE, KDE Plasma, Budgie, UKUI, Trinity TDE, Lumina, EDE, CuteFish, Maui Shell, COSMIC, PaperDE, SonicDE, Liri, Phosh, Plasma Mobile, Glacier, JingOS, Lomiri, Enlightenment, Pantheon.

Текущее состояние: проект в early development, ISO ещё не публиковались. Репозиторий: https://github.com/ObservantJaguar/Zelirion

## Какую wiki надо построить

**Сайт-каталог Zelirion** (Jekyll + Just the Docs, GitHub Pages): страница семейства + полный каталог ISO по платформам и DE + таблицы имён сборок + дорожная карта + техническая документация по build system.

В отличие от энциклопедической wiki, контент здесь — **практический**: какой ISO скачать, что внутри, как собрать, как обновляется.

## Структура (в трёх классах Theory/Tools/Practice — тот же шаблон)

### Theory (концепции)

- **Zelirion overview** — что такое meta-distribution, зачем единая архитектура сборки.
- **Платформы** — Devuan (why no systemd, elogind/eudev/sysvinit/OpenRC), FreeBSD, illumos.
- **X11 vs Wayland** — что поддерживается где (Devuan: X11 полный, Wayland частично; FreeBSD: частично; illumos: без Wayland), Wayland-only DE в X11 fallback.
- **Мобильные DE на десктопе** — Phosh, Plasma Mobile, Glacier, JingOS, Lomiri; концепция «телефон на десктопе».

### Tools (каталог дистрибутивов/ISO)

Структура каталога — по платформам, внутри — по DE. На каждую комбинацию — страница.

**Linux (Devuan):** KDE Plasma (build name Aurora), Xfce (Zentora), LXQt (Quarisa), MATE (Verdina), Cinnamon (Cinnara), Deepin (Divira), Budgie (Avira), UKUI (Kalira), Enlightenment (Enlira), EDE (Edessa), Liri (Lirena), CuteFish (Cutora), Pantheon (Pantara), Lumina (Lumera), Trinity TDE (Trinira), SonicDE (Sonira), Plasma Mobile (Novara), Phosh (Fosira), Glacier (Glafira), Lomiri (Lomira), JingOS (Jingara), PaperDE (Papira), Maui Shell (Mauira).

**FreeBSD:** KDE Plasma (Crestara), Xfce (Valora), LXQt (Arlissa), MATE (Virelina), Lumina (Lumenia), Trinity TDE (Tavira), Enlightenment (Entrisa), UKUI (Kavera), EDE (Edrina).

**illumos:** KDE Plasma (Zalvira), Xfce (Arvessa), LXQt (Sylvira), MATE (Viresta), Trinity TDE (Solviera).

Правила страниц в каталоге:

- Title страницы: `Zelirion <Build Name>` (например `Zelirion Aurora`), а НЕ с маркой «KDE».
- **Торговые марки (GNOME, KDE, Debian и т.д.) не использовать в названиях сборок.** Реальный DE указывается только описательно в тексте/подписи: `DE: KDE Plasma (descriptive reference, not part of the name)`.
- На странице: описание, платформа, DE (подпись), статус сборки, ссылка на скачивание ISO (из Releases), дата релиза, размер, архитектура, требования, screenshot (если есть).
- По каждой платформе — обзорная страница (Devuan/FreeBSD/illumos) с таблицей всех DE-сборок.

### Practice (руководства и документация build system)

- **Build system architecture** — описание модульной схемы сборки (`build/`, `configs/`, `iso/`), как генерируются ISO по DE.
- **Сборка одного ISO** — пошаговый гайд: как собрать конкретную DE (конфиг, live-build на Debian/Devuan).
- **Публикация через GitHub Actions + Releases** — автоматизация: расписание, пересборка при апстрим-обновлении, загрузка в Releases, генерация каталога.
- **Добавление нового DE** — как расширить матрицу (build script, config, имя по схеме).
- **Разработка под мобильные платформы** — GSM/modem stack (ModemManager, ofono, libqmi, libmbim), ARM64.

## Ключевые технические решения (передайте в чат)

### Схема имён сборок (не использующая чужие марки)

Семейство **Zelirion**, каждая сборка — **Zelirion + собственное имя** (Aurora, Zentora, Verdina...). Торговые марки DE — только как описательные подписи, не в названиях. Если в таблице имён из README нет имени для какого-то DE — предложить по схеме: короткое слово, оканчивающееся на -a/-ra/-ara, созвучное DE (например Cinnamon→Cinnara), но не совпадающее с маркой.

### Публикация ISO: GitHub Actions + Releases

- **Releases** — хостинг ISO (до 2 ГБ на файл), ссылки из каталога.
- **GitHub Actions (workflow)** — сборка по расписанию (cron) и по пушу в апстрим-репозитории DE:
  - Проверить новую версию DE (например, релиз KDE Plasma).
  - Запустить build script для этой платформы+DE.
  - Загрузить готовый ISO в Releases с тегом, соответствующим версии.
  - Обновить страницы каталога (генерировать из данных).
- **Лимиты:** ~2000 минут/мес бесплатно на публичный репозиторий; следить за расходом.
- Workflow-файлы — в `.github/workflows/` (YAML).

### Каталог, генерируемый из данных (рекомендация)

Держать матрицу сборок как данные (например `_data/zelirion.yml`): платформа, DE, build name, статус, ссылка на release. Страницы каталога и таблицы — рендерить из этих данных (Liquid), чтобы при апдейте ISO обновлялась одна сущность, а не 20 страниц вручную.

## Процесс

1. Скопируйте `00-template.md` + эту инструкцию в новый чат.
2. Ассистент: (а) изучает репозиторий Zelirion (README, структуру, build-скрипты), (б) проектирует структуру wiki-каталога, (в) создаёт репозиторий/папку сайта по шаблону.
3. Наполнение: overview → платформы → каталог DE (по данным) → практические гайды по сборке.
4. Настройка GitHub Actions workflow для сборки/публикации ISO.
5. Прогон чек-листа из шаблона (ссылки, front matter, кодировка, сборка) и push.