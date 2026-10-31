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

**История изменений:** [CHANGELOG.md](https://github.com/evgenyzh/iinv-xray-releases/blob/main/CHANGELOG.md) ·
[все релизы](https://github.com/evgenyzh/iinv-xray-releases/releases)

<!-- latest:start -->
**Последний релиз / Latest release:** [IINV 3.2.2](https://github.com/evgenyzh/iinv-xray-releases/releases/tag/v3.2.2) · 2026-10-30

| Вариант | Файл | Размер |
|:--|:--|--:|
| Full · TUN + proxy | [`iinv-v3.2.2.apk`](https://github.com/evgenyzh/iinv-xray-releases/releases/download/v3.2.2/iinv-v3.2.2.apk) | 140.2 MB |
| Lite · proxy only | [`iinv-lite-v3.2.2.apk`](https://github.com/evgenyzh/iinv-xray-releases/releases/download/v3.2.2/iinv-lite-v3.2.2.apk) | 140.1 MB |

SHA-256:

```text
f089a7923b629dbca2983bc6b01333520e3c1681350ad28bdc048e75c36de9e4  iinv-v3.2.2.apk
601502b28821909f1acfccf5be0f6bf243b98bb29effa17b762bc66049e80313  iinv-lite-v3.2.2.apk
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
- **Восстановление подключения**: после перезагрузки приложение возвращает
  активный TUN- или PROXY-профиль, если это включено. Если восстановить не
  удалось, системный прокси снимается и интернет работает напрямую. Для TUN
  поддерживается системный Always-on VPN.
- **Автозапуск и батарея**: подсказки для Xiaomi/Redmi/POCO, Huawei/Honor,
  Oppo/Realme/OnePlus, Vivo/iQOO и Samsung, а также карточка состояния батареи.
- **Обновление подписки**: ночное автообновление, проверка конфигурации перед
  применением, откат при ошибке и уведомления.
- **Геоданные**: автоматическая загрузка `geoip.dat`/`geosite.dat` с прогрессом
  и проверкой целостности.
- **Бэкап**: экспорт и импорт профилей, настроек и geo-источников.
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
| Восстановление после перезагрузки | да | да |
| Always-on VPN (Android) | да | — |
| Автозапуск и батарея | да | да |
| Мастер разрешений Shizuku/ADB | да | да |
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

**Changelog:** [CHANGELOG.md](https://github.com/evgenyzh/iinv-xray-releases/blob/main/CHANGELOG.md) ·
[all releases](https://github.com/evgenyzh/iinv-xray-releases/releases)

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
- **Connection recovery**: after a reboot the app restores the active TUN or
  PROXY profile when the setting is enabled. If recovery fails, the system proxy
  is cleared and the internet works directly. TUN supports Android Always-on VPN.
- **Autostart and battery**: guidance for Xiaomi/Redmi/POCO, Huawei/Honor,
  Oppo/Realme/OnePlus, Vivo/iQOO and Samsung, plus a battery state card.
- **Subscription updates**: nightly auto-update, config validation before apply,
  rollback on failure and notifications.
- **Geodata**: automatic `geoip.dat`/`geosite.dat` download with progress and
  integrity checks.
- **Backup**: export and import profiles, settings and geo sources.
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
| Restore after reboot | yes | yes |
| Always-on VPN (Android) | yes | — |
| Autostart and battery | yes | yes |
| Shizuku/ADB permission wizard | yes | yes |
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
