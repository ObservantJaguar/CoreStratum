# Тематическая инструкция: wiki «Дистрибутивы и рабочие столы»

> **Как использовать:** объедините с общим шаблоном `00-template.md` — сначала шаблон (структура, конфиги, правила кодировки), затем эта тематическая часть. Скопируйте в новый чат MultiTool.

## Тема и назначение

Постройте англоязычную wiki-энциклопедию о **Linux/FreeBSD/illumos дистрибутивах** и **окружениях рабочего стола (Desktop Environments)**. Категории: серверные дистрибутивы, десктопные, специализированные; все основные DE (GNOME, KDE Plasma, Xfce, LXQt, Cinnamon, MATE, i3wm/wayland-композиторы и т.д.). Для администраторов, инженеров и энтузиастов open-source.

## Важные принципы содержания

- **Дистрибутив** — это не «ПО», а цельная операционная система: ядро + пакетный менеджер + окружение + сообщество. Страницу строить вокруг: семейство, пакетный менеджер, init system, целевая аудитория, особенности, минимальные требования.
- **DE/WM** — отдельные программы для пользовательского интерфейса (GNOME Shell, KWin, Mutter/Wayland...). У каждого DE — компоненты (композитор, файловый менеджер, эмодзи нет, терминал).
- Разделяйте: дистрибутив, DE, window manager (WM). Не смешивать.
- Помечайте статус: active/спящий, стабильный/rolling, официальный/community, open-source/с проприетарными драйверами.

## Структура в трёх классах

### Theory (теория и концепции)

- **Linux basics** — ядро, дистрибутив, bootloader, init system, пакетные менеджеры (dpkg/apt, rpm/dnf, pacman, zypper).
- **Семейства дистрибутивов** — Debian-семейство, Red Hat/Fedora-семейство, Arch, Gentoo, SUSE; независимые (Alpine, NixOS, Void).
- **FreeBSD и illumos** — история, отличия (jails, ZFS, pf), когда использовать.
- **X11 vs Wayland** — протоколы отображения, композиторы, совместимость, XWayland.
- **Desktop environments vs window managers** — что такое DE, что такое WM (stacking/tiling), compositor, сессии.
- **Display servers и композиторы** — Xorg, Weston, Mutter, KWin, sway/hyprland (Wayland).

### Tools (энциклопедия дистрибутивов и DE)

**Категория «Distributions»** (по семействам):

- **Debian family**: Debian, Ubuntu (LTS/desktop/server), Linux Mint, LMDE, Devuan, MX Linux, Kali, Raspberry Pi OS, Parrot, PureOS.
- **Red Hat family**: RHEL, Fedora, CentOS Stream, Rocky Linux, AlmaLinux, Oracle Linux.
- **Arch family**: Arch Linux, EndeavourOS, CachyOS, Manjaro.
- **Independent**: Alpine, NixOS, Void, Solus, Gentoo, openSUSE (Tumbleweed/Leap), Slackware, Qubes OS (security), Tiny Core.
- **BSD/illumos**: FreeBSD, OpenBSD, NetBSD, DragonFly BSD, GhostBSD; illumos (OpenIndiana, SmartOS), TrueNAS CORE.

**Категория «Desktop Environments»** (каждая страница — DE со списком компонентов):

- GNOME, KDE Plasma, Xfce, LXQt, LXDE, MATE, Cinnamon, Budgie, Pantheon, Deepin DE, Trinity, Enlightenment.

**Категория «Window Managers»**:

- Tiling: i3, Sway (Wayland), Hyprland, bspwm, dwm, awesome, river.
- Stacking: Openbox, Fluxbox, IceWM, JWM.

**Категория «Display servers/compositors»**:

- Xorg, Wayland, Weston, Mutter, KWin, sway, Hyprland, picom (compositor X11).

**Категория «Пакетные менеджеры»** (инструменты):

- APT, dpkg, DNF, RPM, pacman, zypper, Portage, xbps, apk, nix; Flatpak, Snap, AppImage (как универсальные форматы).

**Категория «Системные инструменты/утилиты»** (по нашей философии — только программные продукты): systemd, GRUB, systemd-boot, NetworkManager, PulseAudio/PipeWire, etc.

### Practice (практические руководства)

- Как выбрать дистрибутив под сервер/десктоп (чек-лист).
- Установка Ubuntu Server / Debian / Fedora (базовые шаги, разделы, LVM).
- Установка и настройка конкретного DE (например, KDE Plasma или GNOME) на уже стоящий дистрибутив.
- Установка и настройка tiling WM (i3/Sway/Hyprland) — конфигурация.
- Как включить Wayland и чем он отличается на практике.
- Настройка пакетного менеджера (APT/DNF) — репозитории, обновления.
- FreeBSD: установка, jails, ZFS; illumos: зоны, SMF.
- Dual-boot, резервное копирование системы (Timeshift), восстановление.

## Рекомендуемая структура доменов

```
docs/
├── sections/ (theory/tools/practice)
├── theory/          → категории: linux-basics, distro-families, bsd-illumos, x11-wayland, de-vs-wm
├── distributions/
│   ├── debian-family/   (страницы по каждой)
│   ├── redhat-family/
│   ├── arch-family/
│   ├── independent/
│   └── bsd/branch       (или отдельный домен bsd/illumos)
├── desktop-environments/  → gnome, kde-plasma, xfce, cinnamon, ...
├── window-managers/       → i3, sway, hyprland, openbox, ...
├── display-servers/       → xorg, wayland, mutter, kwin, ...
├── package-managers/      → apt, dnf, pacman, flatpak, ...
├── system-tools/          → systemd, grub, networkmanager, pipewire (опционально)
└── guides/                → практические руководства
```

## Ключевые шаблоны страниц

**Дистрибутив:**

```markdown
---
title: <Дистрибутив>
parent: <Семейство>
grand_parent: Tools
---

# <Дистрибутив>

Одно-два предложения: происхождение, на чём основан, цель.

## Key features
- Пакетный менеджер: <apt/dnf/pacman...>
- Init: <systemd/OpenRC...>
- Модель релизов: <stable/rolling>
- Поддерживаемые архитектуры: <amd64, arm64...>
- Целевая аудитория: <server/desktop/embedded/security>

## Resources
- [Официальный сайт](URL)
- [Документация](URL)
```

**Desktop Environment:**

```markdown
---
title: <Название DE>
parent: Desktop Environments
grand_parent: Tools
---

# <Название DE>

Два-три предложения: что это, базовое окружение, ключевые компоненты.

## Key components
- Compositor / display server: Mutter, KWin, ...
- Файловый менеджер: Files (Nautilus), Dolphin, Thunar, ...
- Терминал, настройки, панель/док: ...
- Поддержка Wayland: да/частично/нет

## Resources
- [Официальный сайт](URL)
```

## Процесс

1. Возьмите структуру и конфиги из шаблона `00-template.md`.
2. Создайте TOC (index.md) с доменами выше.
3. Наполняйте партиями: Family → дистрибутивы (списком страниц), DE → страницы, WM → страницы.
4. Прогоните чек-лист: ссылки, front matter, кодировка, сборка.
5. Push на GitHub.