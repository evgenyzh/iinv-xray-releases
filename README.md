<p align="center">
  <img src="assets/icon-512.png" width="96" alt="IINV">
</p>

<h1 align="center">IINV</h1>

<p align="center">
  <a href="https://github.com/evgenyzh/iinv-xray-releases/releases/latest"><img alt="Latest release" src="https://img.shields.io/github/v/release/evgenyzh/iinv-xray-releases?label=release"></a>
  <img alt="Android 8.0+" src="https://img.shields.io/badge/Android-8.0%2B-3DDC84">
</p>

**Русский** · [English](#english)

IINV — Android-клиент для Xray. Работает с вашей подпиской или JSON-конфигом:
системный VPN (TUN) либо локальный SOCKS/HTTP-прокси. Без аккаунтов, рекламы и
трекинга.

<!-- latest:start -->
**Последний релиз / Latest release:** [IINV 3.2.1](https://github.com/evgenyzh/iinv-xray-releases/releases/tag/v3.2.1) · 2026-10-27

| Вариант | Файл | Размер |
|:--|:--|--:|
| Full · TUN + proxy | [`iinv-v3.2.1.apk`](https://github.com/evgenyzh/iinv-xray-releases/releases/download/v3.2.1/iinv-v3.2.1.apk) | 140.1 MB |
| Lite · proxy only | [`iinv-lite-v3.2.1.apk`](https://github.com/evgenyzh/iinv-xray-releases/releases/download/v3.2.1/iinv-lite-v3.2.1.apk) | 140.1 MB |

SHA-256:

```text
8a834fdfb86022019ba6815b48d7b70b3f7d6c3a25b192ab107a407afd774a9a  iinv-v3.2.1.apk
b4070c86342bc35e247a617eb6d25d02954694b627c0ee51140ea5114d405cd9  iinv-lite-v3.2.1.apk
```
<!-- latest:end -->

## Скриншоты

<p align="center">
  <img src="assets/screen-ru-main.png" width="205" alt="Главный экран">
  <img src="assets/screen-ru-profiles.png" width="205" alt="Профили">
  <img src="assets/screen-ru-network.png" width="205" alt="Монитор сети">
  <img src="assets/screen-ru-theme.png" width="205" alt="Настройки темы">
</p>

## Возможности

- **Два режима**: системный VPN (TUN) и локальный SOCKS/HTTP-прокси на одном
  порту.
- **Подписки**: ссылки VLESS, VMess, Trojan, Shadowsocks, SOCKS/HTTP,
  Hysteria2, а также Clash YAML и JSON.
- **Шаблоны конфигурации**: порты, `routing`, DNS и правила сохраняются при
  обновлении подписки.
- **Локальные JSON-правки** не затираются: при обновлении показывается diff,
  можно применить версию провайдера или оставить свою.
- **Автопрокси**: включает системный прокси при подключении. Нужно одноразовое
  разрешение через ADB или Shizuku — [инструкция](https://evgenyzh.github.io/iinv-xray-releases/adb.html).
- **Мастер разрешений**: Shizuku без компьютера или ADB с ПК, подсказки по
  режиму разработчика, Wi-Fi- и USB-отладке, копирование команд.
- **Мониторинг**: статистика трафика, состояние серверов и управление
  балансировщиками.
- **Темы**: режим (авто / светлая / тёмная) и стиль (Techno / Strict)
  настраиваются отдельно.
- **Приватность**: без рекламы, аналитики и трекеров; настройки и журналы
  остаются на устройстве.

## Full или Lite

| | Full | Lite |
|---|:---:|:---:|
| Системный VPN (TUN) | да | — |
| Локальный SOCKS/HTTP-прокси | да | да |
| Правила для приложений (App Monitor) | да | — |
| Диагностика и управление через adb | да | — |
| Пакет | `cc.iinv.app` | `cc.iinv.app.lite` |

## Установка

1. Скачайте APK из блока «Последний релиз» или со страницы
   [релизов](https://github.com/evgenyzh/iinv-xray-releases/releases).
2. Если Android попросит, разрешите установку из этого источника.
3. Откройте APK и установите. Приложение не предоставляет серверы: нужна ваша
   подписка или JSON-конфиг.
4. Требуется Android 8.0 или новее.

Для автопрокси (автоматическая установка системного прокси) нужно одноразовое
разрешение через ADB или Shizuku — [инструкция](https://evgenyzh.github.io/iinv-xray-releases/adb.html). Без него используйте TUN-режим
(Full) или настройте прокси в Wi-Fi вручную.

Проверка целостности:

```bash
sha256sum -c SHA256SUMS.txt
```

## Приватность

Приложение не собирает и не передаёт персональные данные. Настройки, профили и
журналы хранятся только на устройстве. Политика конфиденциальности:
[privacy.html](https://evgenyzh.github.io/iinv-xray-releases/privacy.html).

---

## English

IINV is an Android client for Xray. It works with your own subscription or JSON
config: system-wide VPN (TUN) or a local SOCKS/HTTP proxy. No accounts, ads or
tracking.

<p align="center">
  <img src="assets/screen-en-main.png" width="205" alt="Home screen">
  <img src="assets/screen-en-profiles.png" width="205" alt="Profiles">
  <img src="assets/screen-en-network.png" width="205" alt="Network monitor">
  <img src="assets/screen-en-theme.png" width="205" alt="Theme settings">
</p>

### Features

- **Two modes**: system VPN (TUN) and a local SOCKS/HTTP proxy on the same port.
- **Subscriptions**: VLESS, VMess, Trojan, Shadowsocks, SOCKS/HTTP and Hysteria2
  links, plus Clash YAML and JSON.
- **Config templates**: ports, `routing`, DNS and rules survive subscription
  updates.
- **Local JSON edits** are preserved: an update shows a diff, so you can apply
  the provider version or keep yours.
- **Auto-proxy**: sets the system proxy when the connection starts. Requires a
  one-time ADB or Shizuku grant — [instructions](https://evgenyzh.github.io/iinv-xray-releases/adb.html#english).
- **Permission wizard**: Shizuku without a computer or ADB with a PC, with hints
  for developer options, wireless/USB debugging and copyable commands.
- **Monitoring**: traffic stats, server state and balancer control.
- **Themes**: mode (auto / light / dark) and style (Techno / Strict) are
  configured separately.
- **Privacy**: no ads, analytics or trackers; settings and logs stay on the
  device.

### Full or Lite

| | Full | Lite |
|---|:---:|:---:|
| System VPN (TUN) | yes | — |
| Local SOCKS/HTTP proxy | yes | yes |
| Per-app proxy rules (App Monitor) | yes | — |
| adb diagnostics and control | yes | — |
| Package | `cc.iinv.app` | `cc.iinv.app.lite` |

### Install

1. Download an APK from the latest release block above or from
   [releases](https://github.com/evgenyzh/iinv-xray-releases/releases).
2. Allow installing from this source if Android asks.
3. Open and install. The app does not provide servers: bring your own
   subscription or JSON config.
4. Android 8.0 or newer is required.

Auto-proxy (setting the system proxy automatically) needs a one-time ADB or Shizuku grant
— [instructions](https://evgenyzh.github.io/iinv-xray-releases/adb.html#english). Without it, use TUN mode (Full) or configure the
proxy in Wi-Fi manually.

Verify integrity:

```bash
sha256sum -c SHA256SUMS.txt
```

Privacy policy:
[privacy.html](https://evgenyzh.github.io/iinv-xray-releases/privacy.html).
