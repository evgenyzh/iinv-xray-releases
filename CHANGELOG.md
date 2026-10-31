# Changelog

Одна секция на версию: `## <версия> — <дата>`, внутри блоки `### Русский` и
`### English`. Секция попадает в описание GitHub-релиза и в публичный
репозиторий `evgenyzh/iinv-xray-releases`.

История с 1.0.0. Секции 1.0.0–2.5.6 восстановлены по git-тегам, сообщениям
коммитов и `MEMORY_BANK.md`: оригинальные тексты релизов не сохранились.
Секции 2.5.7 и новее — исходные release notes; 3.0.0 дополнена по истории
коммитов. Даты — по датам тегов.

## 3.2.2 — 2026-10-30

### Русский

- Уведомление сервиса стало нейтральным: «Сервис» / «Работает в фоне», без
  кнопки «Остановить»; на экране блокировки содержимое скрыто.
- Переключение на TUN-профиль запрашивает системное VPN-разрешение; если
  разрешение не выдано, приложение показывает ошибку, а не падает.
- Сервис поднимает foreground-уведомление до создания TUN, поэтому ошибки
  запуска больше не приводят к `RemoteServiceException`.
- На Huawei/Honor кнопка «Автозапуск» открывает «Батарея → Запуск приложений»
  вместо информации о приложении.
- Восстановление после обновления приложения стало надёжнее: состояние запуска
  хранится отдельно от перезаписываемых настроек, а активный профиль берётся из
  снимка соединения.
- Перед восстановлением после обновления системный прокси снимается; если
  восстановить соединение не удалось, интернет продолжает работать напрямую.
- На Android 10 в ADB-мастере больше не показывается примечание про Shizuku.
- После перезагрузки приложение удерживает boot-receiver до запуска сервиса,
  поэтому отложенный `BOOT_COMPLETED` (например, на MIUI после разблокировки)
  не теряется.
- Добавлена общая настройка «Восстанавливать после перезагрузки» для TUN и
  PROXY. Если она выключена, системный прокси всё равно снимается, а
  приложение остаётся отключённым.
- До разблокировки устройства отдельный receiver (`LOCKED_BOOT_COMPLETED`)
  снимает системный прокси, чтобы после сбоя питания интернет не оставался
  привязанным к неработающему локальному порту.
- Восстановление после загрузки повторяется в свежем процессе сервиса через
  30 и 90 секунд; повтор не выполняется, если пользователь уже отключился.
- Для TUN проверяется VPN-разрешение, а для PROXY — что локальный порт уже
  слушает, и только после этого выставляется системный прокси.
- Добавлена поддержка системного Always-on VPN для TUN: Android сам запускает
  сервис и туннель после загрузки, даже если приложение не успело восстановиться
  по `BOOT_COMPLETED`. Отключение в приложении останавливает туннель; полностью
  Always-on выключается в системных настройках VPN.
- Boot-receiver остаётся best-effort: на EMUI доставка `BOOT_COMPLETED` не
  гарантируется; Always-on VPN является системным путём для таких устройств.
- «Восстанавливать после перезагрузки» и постоянная VPN Android собраны в один
  раздел «Восстановление подключения»; в lite постоянная VPN не показывается.

### English

- The service notification is neutral: "Service" / "Running in background",
  with no Stop action; content is hidden on the lock screen.
- Switching to a TUN profile asks for the system VPN permission; if it is not
  granted, the app shows an error instead of crashing.
- The service posts its foreground notification before creating the TUN
  interface, so start failures no longer cause `RemoteServiceException`.
- On Huawei/Honor the Autostart button opens Battery → App launch instead of
  app info.
- Update recovery is more reliable: the running state is stored outside the
  preferences that can be overwritten, and the active profile is resolved from
  the connection snapshot.
- The system proxy is cleared before an update restore; if the connection cannot
  be restored, the internet keeps working directly.
- On Android 10 the ADB wizard no longer shows the Shizuku note.
- After a reboot the boot receiver stays alive until the service starts, so a
  delayed `BOOT_COMPLETED` (for example on MIUI after unlock) is not lost.
- Added a shared "Restore after reboot" setting for TUN and PROXY. When it is
  off, the system proxy is still cleared and the app stays disconnected.
- Before the device is unlocked, a separate `LOCKED_BOOT_COMPLETED` receiver
  clears the system proxy, so a power loss cannot leave the internet bound to a
  local port that is not running yet.
- Boot restore is retried in a fresh service process after 30 and 90 seconds;
  the retry is skipped if the user has already disconnected.
- TUN checks the VPN permission, and PROXY waits until the local port is
  listening before the system proxy is set.
- Added system Always-on VPN support for TUN: Android starts the service and the
  tunnel after boot, even if `BOOT_COMPLETED` arrives late or not at all.
  Disconnect in the app stops the tunnel; Always-on itself is turned off in the
  system VPN settings.
- The boot receiver remains best-effort: EMUI does not guarantee
  `BOOT_COMPLETED` delivery; Always-on VPN is the system path for such devices.
- "Restore after reboot" and Android Always-on VPN now share one Connection
  recovery section; Always-on is not shown in lite.

## 3.2.1 — 2026-10-27

### Русский

- Подсказки по автозапуску для Xiaomi/Redmi/POCO, Huawei/Honor,
  Oppo/Realme/OnePlus и Vivo/iQOO: баннер на главной и карточка в настройках
  ведут в системный экран автозапуска. Подсказка показывается один раз после
  установки, сама настройка сохраняется при обновлениях.
- Для Samsung — отдельная карточка «Фоновая работа» с переходом в настройки
  батареи и подсказкой добавить IINV в «Не спящие приложения».
- После обновления приложения соединение восстанавливается автоматически;
  если поднять сервис не удалось, системный прокси снимается, чтобы интернет
  не пропадал.
- Карточка батареи больше не показывает неактивную кнопку «Открыть настройки»,
  когда ограничений уже нет.

### English

- Autostart guidance for Xiaomi/Redmi/POCO, Huawei/Honor,
  Oppo/Realme/OnePlus and Vivo/iQOO: a home banner and a Settings card open the
  system autostart screen. The hint is shown once after installation; the
  setting itself persists across updates.
- Samsung gets a separate Background work card that opens battery settings and
  points to Never sleeping apps.
- After an app update the connection is restored automatically; if the service
  cannot be started, the system proxy is cleared so the internet keeps working.
- The battery card no longer shows an inactive "Open settings" button when no
  restrictions remain.

## 3.2.0 — 2026-10-27

### Русский

- Мастер разрешений: на первом экране выбор — Shizuku без компьютера или ADB
  с компьютером. Для Shizuku приложение само проверяет режим разработчика и
  «Отладку по Wi-Fi», помогает открыть нужный экран и только потом запускает
  Shizuku.
- Установка Shizuku из Google Play или с GitHub; запуск через Wi-Fi-отладку или
  USB. Разрешения `WRITE_SECURE_SETTINGS` и usage stats выдаёт Shizuku-сервис,
  без Termux и ручных команд.
- Запасной ADB-путь: пошаговые команды с копированием одной кнопкой; карточка
  «Для продвинутых» убрана из «Сети».
- Баннер на главной и кнопка в настройках сети помогают включить автопрокси.
  «Позже» скрывает баннер до следующего дня, «Не показывать» — навсегда.
- App Monitor: при попытке включить без доступа открывается мастер; после
  выдачи правила включаются автоматически.
- Помощник по отладке: открывает «О телефоне» и «Для разработчиков», показывает
  состояние режима разработчика, Wi-Fi- и USB-отладки, подсказывает про
  MIUI/HyperOS.
- «Обслуживание» стало «Настройками»: тема, язык, батарея, обновления, бэкап,
  диагностика и ассистенты собраны по группам. Split tunnel показывается только
  для TUN-профилей, сохранённые значения не сбрасываются.
- После мастера автопрокси включается сразу; если соединение уже активно в
  режиме PROXY, системный прокси применяется без переподключения.
- Новые иконки запуска и диалоги с outline во всех палитрах.

### English

- Permission wizard: the first screen chooses Shizuku without a computer or ADB
  with one. For Shizuku the app checks developer options and Wireless debugging,
  helps open the right screen and only then starts Shizuku.
- Install Shizuku from Google Play or GitHub; start it through Wireless debugging
  or USB. The Shizuku service grants `WRITE_SECURE_SETTINGS` and usage access
  without Termux or manual commands.
- ADB fallback: step-by-step commands with one-tap copy; the "For advanced"
  card is gone from Network.
- A home banner and a Network settings button help enable auto-proxy. "Later"
  hides the banner until the next day; "Don't show" hides it permanently.
- App Monitor: enabling it without usage access opens the wizard; the monitor is
  enabled automatically after the grant.
- Debugging helper: opens About phone and Developer options, shows developer
  mode, wireless and USB debugging state, and includes the MIUI/HyperOS hint.
- Maintenance is now Settings: theme, language, battery, updates, backup,
  diagnostics and assistants are grouped. Split tunneling is shown only for TUN
  profiles and saved values are preserved.
- Auto-proxy is enabled after the wizard; if a PROXY-mode connection is already
  active, the system proxy is applied without reconnecting.
- New launcher icons and outlined dialogs in every palette.

## 3.1.1 — 2026-10-25

### Русский

- Новый разбор подписок: ссылки VLESS, VMess, Trojan, Shadowsocks, SOCKS/HTTP,
  Hysteria2, а также Clash YAML. Конфигурация собирается и проверяется перед
  сохранением профиля.
- Шаблоны конфигурации: порты SOCKS/HTTP, `routing`, `dns`, `policy`, `log` и
  собственные outbounds сохраняются при обновлении подписки.
- Локальные правки JSON больше не затираются: при изменении JSON-подписки
  показывается diff с выбором «Применить» или «Оставить локальную».
- Уведомление об изменении подписки.
- Режим темы (авто / светлая / тёмная) и стиль (Techno / Strict) настраиваются
  отдельно.
- Исправлены split tunneling в TUN, отображение состояния батареи, готовность
  балансировщика и возврат назад.
- Обновлены палитры, включая Techno Dark.

### English

- New subscription parser: VLESS, VMess, Trojan, Shadowsocks, SOCKS/HTTP and
  Hysteria2 links, plus Clash YAML. Configs are assembled and validated before
  the profile is saved.
- Config templates keep SOCKS/HTTP ports, `routing`, `dns`, `policy`, `log` and
  custom outbounds across subscription updates.
- Local JSON edits are no longer overwritten: a JSON subscription change shows
  a diff and lets you apply the provider version or keep yours.
- Subscription change notifications.
- Theme mode (auto / light / dark) and palette style (Techno / Strict) are now
  configured separately.
- Fixed TUN split tunneling, battery state display, balancer readiness and back
  navigation.
- Refreshed palettes, including Techno Dark.

## 3.0.0 — 2026-10-25

### Русский

- Новый интерфейс Plex Mono: четыре вкладки, новые палитры и светлая/тёмная тема.
- Экран журналов и действие «Очистить логи».
- В full-сборке: диагностика и управление через adb (`iinvctl`), opt-in
  управление агентом, AppFunctions и ассистенты.
- Геоданные: источник по умолчанию `evgenyzh/xray-geodata`, проверка ETag и
  SHA-256.
- Ночное автообновление подписки с проверкой, откатом и уведомлениями.
- Ограничение и очистка журналов.

### English

- New Plex Mono interface: four tabs, new palettes and light/dark themes.
- Logs screen and a "Clear logs" action.
- Full build only: adb diagnostics and control (`iinvctl`), opt-in agent
  control, AppFunctions and assistants.
- Geodata: the default source is `evgenyzh/xray-geodata`, with ETag and SHA-256
  checks.
- Nightly subscription auto-update with validation, rollback and notifications.
- Log retention and manual clearing.

## 2.6.1 — 2026-10-24

### Русский

- Переключение профилей теперь запускает xray только в свежем процессе
  `:netsvc`: остановка, завершение процесса, затем запуск. Состояние
  предыдущего конфига больше не влияет на новый.
- Команды старта и остановки сериализованы; добавлены проверка закрытия
  listener'а, watchdog остановки на 4 секунды и снятие системного прокси до
  остановки native-ядра.
- gRPC-канал статистики обходит системный прокси; счётчики трафика сбрасываются
  при смене профиля или подключения.
- В журнал пишется выбранный xray uTLS fingerprint для `random`.
- Проверка tun-inbound учитывает runtime-имя интерфейса, поэтому Android 14+
  больше не показывает ложное «Invalid» для рабочих конфигов.
- Состояние `wasRunning` и активный профиль сохраняются синхронно, состояние
  обновляется при возврате в приложение, а журналы UI и `:netsvc` не
  перезаписывают друг друга.

### English

- Profile switching now starts xray only in a fresh `:netsvc` process: stop,
  process death, then start. State from the previous config no longer leaks into
  the new one.
- Start and stop commands are serialized; listener shutdown is verified, a
  4-second stop watchdog is added, and the system proxy is cleared before the
  native core stops.
- The stats gRPC channel bypasses the system proxy; traffic counters are reset
  when the profile or connection changes.
- The uTLS fingerprint xray picks for `random` is written to the log.
- TUN inbound validation uses the runtime interface name, so Android 14+ no
  longer reports a false "Invalid" for working configs.
- `wasRunning` and the active profile are persisted synchronously, state is
  refreshed when the app returns, and the UI and `:netsvc` app logs no longer
  overwrite each other.

## 2.6.0 — 2026-10-24

### Русский

- xray-core обновлён до 26.10.21 (libxray v1.261021.0).
- Native-сборка переведена на Go 1.27.3; в builder добавлены build-tools 35.
- Технический выпуск: интерфейс и настройки не менялись.

### English

- xray-core updated to 26.10.21 (libxray v1.261021.0).
- The native build moved to Go 1.27.3; build-tools 35 were added to the builder.
- Technical release: the UI and settings are unchanged.

## 2.5.7 — 2026-10-16

### Русский

- В подписи «Since» показывается дата для давних подключений.
- Подсказка про APN и мобильную сеть в ручной настройке прокси.
- Исправлен верхний отступ главного экрана на устройствах с вырезом.

### English

- The "Since" label shows the date for long-running connections.
- APN and cellular network hint in the manual proxy setup.
- Fixed the main screen top inset on devices with a cutout.

## 2.5.6 — 2026-10-16

### Русский

- Исправлен белый экран при быстрых повторных нажатиях «Назад»: переход
  выполняется только из текущего экрана, а корневой экран закрывает приложение.
- Docker-сборки читают git-тег, поэтому локальные APK больше не показывают
  ложное обновление 1.0.0.

### English

- Fixed the white screen after rapid repeated Back taps: navigation only pops
  from the current screen, and the root screen finishes the activity.
- Docker builds read the git tag, so local APKs no longer show a false 1.0.0
  update.

## 2.5.5 — 2026-10-16

### Русский

- Геоданные: автозагрузка при старте с прогрессом и кнопкой «Остановить»;
  баннер можно скрыть, скрытие сохраняется, пока файлы не появятся.
- Ручная настройка прокси показывает адрес и порт, копирует адрес и объясняет,
  как прописать прокси в Wi-Fi.
- Разрешение на автопрокси перепроверяется при открытии настроек, поэтому выдача
  через ADB подхватывается без перезапуска приложения.
- Подготовлены отдельные сборки full/lite/tun для Google Play; в Play-сборках
  скрыт GitHub-апдейтер.
- targetSdk 36 и 16 KB page size; TUN запускается без netlink, а список
  приложений работает без `QUERY_ALL_PACKAGES`.

### English

- Geodata: automatic download on startup with progress and a Stop button; the
  banner can be dismissed, and the dismissal persists until the files appear.
- Manual proxy setup shows the address and port, copies the address and explains
  how to configure the proxy in Wi-Fi settings.
- The auto-proxy permission is re-checked when proxy settings open, so an ADB
  grant is picked up without restarting the app.
- Separate full/lite/tun builds were prepared for Google Play; the GitHub
  updater is hidden in Play builds.
- targetSdk 36 and 16 KB page size; TUN starts without netlink, and the app list
  works without `QUERY_ALL_PACKAGES`.

## 2.5.4 — 2026-10-09

### Русский

- Исправлен заголовок версии: приложение больше не показывает «vv2.5.3».

### English

- Fixed the version title: the app no longer shows "vv2.5.3".

## 2.5.3 — 2026-10-09

### Русский

- Сервис сам восстанавливает активный профиль, если система перезапускает его
  после остановки.
- Журнал приложения ротируется один раз за процесс, а не при каждой
  инициализации контроллера.

### English

- The service restores the active profile when the system restarts it after a
  stop.
- The app log rotates once per process instead of on every controller
  initialization.

## 2.5.2 — 2026-10-09

### Русский

- Периодические задачи обновления пересоздаются при изменении интервала:
  WorkManager больше не пропускает запланированные запуски.
- Соединение считается активным только если процесс сервиса действительно жив;
  сохранённый флаг не путает состояние после обновления приложения.
- Уведомление о доступном обновлении снимается при сбросе отложенного конфига.

### English

- Periodic update work is recreated when the interval changes, so WorkManager no
  longer skips scheduled runs.
- A connection counts as running only when the service process is actually
  alive; a stored flag no longer confuses the state after an app update.
- The update-available notification is cleared when a pending config is reset.

## 2.5.1 — 2026-10-09

### Русский

- При применении отложенного обновления перезапускается активный профиль, а не
  тот, которому принадлежит обновление. Обновление больше не переключает
  соединение на другой профиль.

### English

- Applying a pending update restarts the active profile, not the profile the
  update belongs to. An update no longer switches the connection to another
  profile.

## 2.5.0 — 2026-10-09

### Русский

- Переработано обновление конфигураций: синхронизация по расписанию, догоняющий
  запуск при старте, отложенное применение при активном соединении и
  уведомления об успехе или ошибке.
- Шаблоны конфигурации: валидные default-шаблоны full/lite, восстановление
  профилей со старым сломанным default и сохранение пользовательских
  `policy.levels` / `policy.system`.
- Lite всегда работает в режиме PROXY, а TUN-inbounds вырезаются из
  импортированных профилей.
- Native-сборка переведена на libxray Invoke API v3 (v1.260930.0) и Go 1.27.1;
  xray-core обновлён до 26.9.30.

### English

- Config updates were reworked: scheduled sync, startup catch-up, deferred apply
  while connected, and success or failure notifications.
- Config templates: valid full/lite defaults, healing of profiles with the old
  broken default, and preservation of user `policy.levels` / `policy.system`.
- Lite always runs in PROXY mode, and TUN inbounds are stripped from imported
  profiles.
- The native build moved to libxray Invoke API v3 (v1.260930.0) and Go 1.27.1;
  xray-core was updated to 26.9.30.

## 2.4.1 — 2026-05-14

### Русский

- Исправлено подключение к статистике после перезапуска xray: gRPC-канал
  пересоздаётся на новый случайный порт.
- В README описаны lite-сборка и различия full/lite.

### English

- Fixed stats connectivity after an xray restart: the gRPC channel reconnects to
  the new random port.
- The README now documents the lite build and the full/lite differences.

## 2.4.0 — 2026-05-13

### Русский

- Появились две сборки: full (`cc.iinv.app`, TUN + прокси) и lite
  (`cc.iinv.app.lite`, только локальный прокси).
- Lite не запрашивает VPN-разрешение и не содержит TUN.
- Порт gRPC-статистики теперь случайный (45000–60000) и сохраняется в
  `cache/api.port`.
- Release workflow собирает и публикует оба APK.

### English

- Added two builds: full (`cc.iinv.app`, TUN + proxy) and lite
  (`cc.iinv.app.lite`, local proxy only).
- Lite does not request VPN permission and contains no TUN.
- The stats gRPC port is now random (45000–60000) and stored in
  `cache/api.port`.
- The release workflow builds and publishes both APKs.

## 2.3.1 — 2026-05-09

### Русский

- В списке балансировщика показываются все серверы из конфигурации, а не только
  активный; шаблоны селекторов раскрываются в реальные outbound-теги.
- Отображается стратегия балансировщика.
- Улучшено определение Samsung Knox/Secure Folder: расширен список пакетов,
  обход ограничения Kotlin через reflection.

### English

- The balancer list shows all servers from the config, not only the active one;
  selector patterns are resolved to real outbound tags.
- The balancer strategy is displayed.
- Improved Samsung Knox/Secure Folder detection: expanded package list and a
  Kotlin reflection workaround.

## 2.3.0 — 2026-05-08

### Русский

- Поддержка Samsung Knox Secure Folder: приложения из защищённой папки
  определяются как рабочий профиль и получают отдельные правила.

### English

- Samsung Knox Secure Folder support: apps from the secure folder are detected
  as a work profile and get separate rules.

## 2.2.1 — 2026-05-03

### Русский

- Исправлено определение рабочего профиля и холодного старта ForegroundMonitor.
- Логика foreground-мониторинга упрощена: состояние определяется по событиям
  background, без таймеров и эвристик.
- Снижено энергопотребление: wake lock только на 30 секунд в TUN, повторное
  использование gRPC-канала, остановка монитора при выключенном экране,
  отложенный boot-start и battery constraints для WorkManager.
- Ручная проверка обновлений выполняется всегда; троттлинг остался только для
  автоматической проверки.
- Рефакторинг: общие `AppPaths`, `AppJson`, `HttpClient`, `AppPreferences`;
  удалён мёртвый код.
- Версия 2.2.0 не получила отдельный тег; её изменения вошли в 2.2.1.

### English

- Fixed work profile detection and ForegroundMonitor cold start.
- Foreground monitoring was simplified: state is derived from background events,
  without timers or heuristics.
- Lower energy use: a 30-second wake lock in TUN, gRPC channel reuse, monitor
  pause while the screen is off, delayed boot start and battery constraints for
  WorkManager.
- Manual update checks always run; throttling now applies only to automatic
  checks.
- Refactoring: shared `AppPaths`, `AppJson`, `HttpClient` and `AppPreferences`;
  dead code removed.
- Version 2.2.0 never got a separate tag; its changes shipped in 2.2.1.

## 2.1.1 — 2026-05-02

### Русский

- Технический выпуск: исправлено имя публичного репозитория и повторный запуск
  release workflow; изменений в приложении нет.

### English

- Technical release: fixed the public repository name and release workflow
  re-runs; no app changes.

## 2.1.0 — 2026-05-02

### Русский

- Проверка обновлений внутри приложения через GitHub Releases: баннер на
  главной, пропуск версии и автопроверка не чаще раза в 24 часа.
- Новый экран Maintenance: обновления, экспорт/импорт и журналы.
- Автообновление конфигурации: сравнение хэша, остановка xray, валидация и
  перезапуск; при ошибке старый конфиг сохраняется.
- Кнопка Validate недоступна при активном соединении.
- Новые иконки IINV и adaptive icon.

### English

- In-app update checks via GitHub Releases: a home banner, version skipping and
  automatic checks no more than once every 24 hours.
- New Maintenance screen: updates, export/import and logs.
- Config auto-update: hash comparison, stop xray, validation and restart; the old
  config is kept if validation fails.
- The Validate button is disabled while connected.
- New IINV icons and adaptive icon.

## 2.0.0 — 2026-05-02

### Русский

- Ребрендинг: `com.iinv.xray` → `cc.iinv.app`, `libxray.so` → `libnetsvc.so`,
  процесс `:xray` → `:netsvc`.
- TUN и PROXY объединены в один `NetworkService`; VPN-разрешение запрашивается
  только для TUN.
- Обновлены темы, ProGuard и proto-пакеты.
- Версия 1.4.0 не получила отдельный тег; ребрендинг вышел в 2.0.0.

### English

- Rebranding: `com.iinv.xray` → `cc.iinv.app`, `libxray.so` → `libnetsvc.so`,
  process `:xray` → `:netsvc`.
- TUN and PROXY were merged into one `NetworkService`; VPN permission is
  requested only for TUN.
- Updated themes, ProGuard rules and proto packages.
- Version 1.4.0 never got a separate tag; the rebranding shipped in 2.0.0.

## 1.3.4 — 2026-05-01

### Русский

- На главном экране показывается режим профиля (TUN/SOCKS), а не URL.

### English

- The home screen shows the profile mode (TUN/SOCKS) instead of the URL.

## 1.3.3 — 2026-05-01

### Русский

- Технический выпуск: подавлены deprecation warnings, кэширован Json, иконки
  переведены на AutoMirrored.

### English

- Technical release: deprecation warnings suppressed, Json cached, and icons
  moved to AutoMirrored.

## 1.3.2 — 2026-05-01

### Русский

- Технический выпуск: release workflow создаёт релиз и в приватном репозитории.

### English

- Technical release: the release workflow also creates a release in the private
  repository.

## 1.3.1 — 2026-05-01

### Русский

- Исправлен ProGuard: поля protobuf-запросов балансировщика больше не
  обфусцируются, запросы работают в release-сборке.
- Контент больше не перекрывается системной навигационной панелью.

### English

- Fixed ProGuard: protobuf balancer request fields are no longer obfuscated, so
  requests work in release builds.
- Content no longer overlaps the system navigation bar.

## 1.3.0 — 2026-04-30

### Русский

- Статистика трафика xray через gRPC: inbounds, outbounds и users,
  автообновление и сброс счётчиков.
- Экран Network Monitor: состояние серверов и управление балансировщиками
  (Auto/Manual, выбор outbound).
- Кнопка статистики на главном экране при активном соединении.

### English

- xray traffic statistics over gRPC: inbounds, outbounds and users,
  auto-refresh and counter reset.
- Network Monitor screen: server state and balancer control (Auto/Manual,
  outbound selection).
- A stats button on the home screen while connected.

## 1.2.1 — 2026-04-30

### Русский

- Технический выпуск: release workflow публикует APK в публичный репозиторий
  релизов.

### English

- Technical release: the release workflow publishes APKs to the public releases
  repository.

## 1.2.0 — 2026-04-30

### Русский

- App Monitor: debounce, настраиваемый интервал опроса и отладочный журнал.
- Экспорт и импорт профилей, настроек и geo-источников в JSON.
- Исправлен default config: direct passthrough вместо нерабочего
  VLESS+REALITY.
- Прогресс скачивания геоданных.

### English

- App Monitor: debounce, configurable poll interval and debug logging.
- Export and import of profiles, settings and geo sources as JSON.
- Fixed the default config: direct passthrough instead of the broken
  VLESS+REALITY template.
- Geodata download progress.

## 1.1.2 — 2026-04-28

### Русский

- Определение foreground-приложения по событиям каждого пакета; краткие
  оверлеи больше не переключают прокси.
- Переключатель определения рабочего профиля (по умолчанию выключен) и
  предупреждение об эвристике.

### English

- Foreground app detection now tracks events per package; brief overlays no
  longer switch the proxy.
- A work profile detection switch (off by default) and a warning about the
  heuristic.

## 1.1.1 — 2026-04-27

### Русский

- App Monitor: правила ON / без изменений / OFF для каждого приложения,
  отдельный экран и правила для рабочего профиля.
- Состояние прокси замораживается при выключении экрана и восстанавливается при
  включении.
- Geo-баннер на главной с кнопками «Скачать» и «Скрыть».
- Исправлены краш DataStore и игнорирование собственного приложения.

### English

- App Monitor: ON / no change / OFF rules per app, a dedicated screen and work
  profile rules.
- Proxy state is frozen when the screen turns off and restored when it turns on.
- A geodata banner on the home screen with Download and Dismiss actions.
- Fixed the DataStore crash and the app ignoring itself.

## 1.1.0 — 2026-04-27

### Русский

- Автоматическая установка системного прокси при подключении (требуется
  `WRITE_SECURE_SETTINGS`).
- Исправлена работа с рабочим профилем.

### English

- Automatic system proxy configuration when a connection starts (requires
  `WRITE_SECURE_SETTINGS`).
- Fixed work profile handling.

## 1.0.3 — 2026-04-26

### Русский

- Технический выпуск: исправлены broadcast-типы состояния VPN после R8.

### English

- Technical release: fixed VPN state broadcast types after R8.

## 1.0.2 — 2026-04-26

### Русский

- Технический выпуск: удалён WorkManagerInitializer из манифеста.

### English

- Technical release: removed WorkManagerInitializer from the manifest.

## 1.0.1 — 2026-04-26

### Русский

- Пересборка 1.0.0 без изменений кода.

### English

- Rebuild of 1.0.0 with no code changes.

## 1.0.0 — 2026-04-26

### Русский

- Первый публичный выпуск.
- TUN-режим через `VpnService` и локальный SOCKS/HTTP-прокси.
- Профили, импорт JSON-конфигурации и split tunneling.
- Журналы xray и приложения, геоданные, автозапуск после загрузки и keep-alive
  при активном соединении.

### English

- First public release.
- TUN mode via `VpnService` and a local SOCKS/HTTP proxy.
- Profiles, JSON config import and split tunneling.
- xray and app logs, geodata, start on boot and keep-alive while connected.
