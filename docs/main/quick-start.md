# Быстрый старт

## Основная информация

### Где скачать ALT Regular Gnome?

Загрузить ISO образ дистрибутива можно по ссылкам: [x86_64](https://mirror.yandex.ru/altlinux-nightly/tested/regular-gnome-latest-x86_64.iso), [aarch64](https://nightly.altlinux.org/sisyphus-aarch64/tested/regular-gnome-latest-aarch64.iso)

### Какие DE поддерживаются?

Текущий выпуск **ALT Regular Gnome** поддерживает рабочее окружение GNOME 47

### Как часто обновляется в репозитории Сизиф версия рабочего окружения GNOME?

Обновление мажорной версии рабочего окружения происходит два раза в год: весной и осенью. После выпуска стабильной версии производителем рабочего окружения GNOME, происходит обновление в репозитории Сизиф, как правило в течение недели. Аналогично происходит обновление минорных версий рабочего окружения, пользователь репозитория получает большинство обновлений в течение недели.

### Можно ли понизить версию рабочего окружения, к примеру до версии 44?

Рабочее окружение GNOME имеет большое количество зависимостей с системными библиотеками (среди аналогичных DE этот список один из самых больших), данные библиотеки поставляются с операционной системой. Для корректной работы GNOME существует определённый перечень библиотек с перечнем ограничений по версиям. В связи с данными техническими особенностями невозможно понизить версию рабочего окружения в ALT Regular GNOME, как и в большинстве других дистубутивов.

### В чем отличие сборок ALT Regular Gnome и ALT Starterkits Gnome

Основное отличие сборок репозиторий:

- **ALT Regular Gnome** основан на базе репозитория Сизиф
- **ALT Starterkits Gnome** основан на базе на стабильном бранче P11

Как следствие, отличается версия рабочего окружения:

- **ALT Regular Gnome** версия рабочего окружения GNOME 47.x
- **ALT Starterkits Gnome** версия рабочего окружения GNOME 46.x

### Я нашёл ошибку в программе. Как мне сообщить о ней?

Необходимо создать тикет в [ALT Linux BugZilla](https://bugzilla.altlinux.org) для проблемного компонента и подробно описать суть возникшей проблемы на английском языке.
При необходимости разработчики могут запросить более подробную информацию, а также журналы работы системы.

### У меня возникло затруднение. Где я могу получить помощь?

Вы всегда можете обратиться за помощью к другим участникам сообщества.

Чаты в Telegram:

[ALT Regular Gnome](https://t.me/alt_gnome_chat) – основной чат ALT Regular Gnome на русском языке;

## Пакетный менеджер и установка пакетов

### Какой менеджер пакетов используется в ALT Regular Gnome?

По умолчанию, используется пакетный менеджер [apt](apt-get), альтернативным вводом является единая команда управления пакетами [epm](epm).

#### Почему apt-get, а не apt?

В операционных системах семейства Альт используется порт-версия пакетного менеджера АРТ. Порт-версия обычно включает модификации, и в нашем случае это возможность работы с RPM-пакетами при максимальном сохранении пользовательских свойств исходного приложения.

Во время активной разработки порт-версии командный интерфейс в пакете APT отсутствовал. Полномочия за синхронизацию свойств пользователей и внесение улучшений из основного репозитория APT лежит на участниках порт-версии.

### Поддерживается установка Flatpak-пакетов?

`Flatpak` – это прогрессивный формат самодостаточных пакетов для GNU/Linux. Данный способ полностью совместим с **ALT Regular Gnome**, для использования [необходимо установить приложения и подготовить его к работе](/flatpak).

### Как правильно обновлять систему?

**ALT Regular Gnome** поддерживает два вида обновлений: через консоль средствами пакета `apt-get`, либо через графические менеджеры, основанные на PackageKit. Мы рекомендуем установить Центр приложений (GNOME Software)

Обновление системы средствами `apt-get` и `epm`:

::: code-group

```shell[apt-get]
su -
apt-get update
apt-get dist-upgrade
```

```shell[epm]
epm Upgrade
```

:::

#### Полное обновление системы командой `epm full-upgrade`

Команда `epm full-upgrade` помимо пакетов позволяет обновить также ядро системы, пакеты установленные через [epm play](https://alt-gnome.wiki/epm.html#утилита-epm-play), а также Flatpak-приложения:

Использование:

```shell
su -
epm full-upgrade
```

Предварительно также можно сделать снимок системы с помощью [Timeshift](https://alt-gnome.wiki/timeshift.html) командой:

```shell
timeshift --create
```

При этом настоятельно не рекомендуется запускать процесс в эмуляторах терминала графической среды. Обновления системы приходят ежедневно. Мы рекомендуем устанавливать обновления системы ежедневно.

### Можно ли скачать, но не устанавливать пакет из репозитория?

Скачивание пакета foo-bar в текущий рабочий каталог:

```shell
su -
apt-get -d install foo-bar
```

### Безопасно ли использовать основанные на PackageKit модули обновления из графического режима?

Да, использование графических менеджеров, основанных на PackageKit (рекомендуем GNOME Software), для обновления системы из графического режима полностью безопасно, т.к. они сначала скачивают файлы обновлений в свой кэш, а для непосредственной установки уже используют специальный сервис. В случае падения GUI приложения, никаких повреждений не будет.

### Как автоматически удалить ненужные более пакеты?

`Apt-get` автоматически удаляет зависимости, не нужные более для работы установленных пакетов, однако этот процесс можно инициировать и вручную:

```shell
su -
apt-get autoremove
```

Следует соблюдать максимальную осторожность при использовании данной команды, т.к. это может повлечь за собой удаление важных, но автоматически установленных компонентов рабочей среды.

Если какие-либо из кандидатов необходимы для дальнейшей работы, их лучше всего пометить как установленные пользователем.

### Как мне переустановить пакет?

Для переустановки пакета или пакетов можем воспользоваться штатной функцией `reinstall` из пакета `apt-get`.

Переустановим пакет foo-bar:

```shell
su -
apt-get reinstall foo-bar
```

## Работа в системе

### Почему `sudo` не работает из коробки?

Образ ALT Regular Gnome выполняет несколько задач, к примеру использование актуальной версии рабочего окружения GNOME, однако все образы семейства ALT Regular предоставляют возможность простого создания производных дистрибутивов, безусловно это накладывает ряд ограничений по базовой конфигурации образа, но пользователю предоставляется возможность настроить [sudo](/sudo) самостоятельно.

Штатным способом временного получения прав `root` в операционных системах семейства «Альт», является команда `su -`. Команда `sudo` в большинстве продуктов семейства «Альт» требует предварительной настройки, так как в `/etc/sudoers` не описан ни один пользователь, включая `root`.

Сделано это из соображений безопасности, поскольку после выполнения `sudo` существует временной отрезок, в течение которого повторное выполнение команды `sudo` не требует пароль (что может быть использована для взлома вашего компьютера со стороны руткитов и хакерских атак).

### Что такое TTY, как войти, как выйти?

TTY, сокращение от Teletypewriter, представляет собой интерфейс командной строки без использования графического интерфейса, в котором вы можете управлять своей операционной системой, набирая команды.

Для перехода в интерфейс TTY, используйте комбинацию [[Ctrl]] + [[Alt]] + ([[F3]] - [[F6]]), для использования необходима авторизация. Для возврата к основному дисплею используйте комбинацию [[Ctrl]] + [[ALT]] + [[F2]], если вы не авторизованы, перейдите на экран входа [[Ctrl]] + [[Alt]] + [[F1]]

### Как показать процент заряда батареи?

Зайдите в приложение «Настройки», перейдите в панель «Питание», активируйте настройку «Показать процент заряда батареи». Альтернативным вариантом является изменение `gsettings`, к примеру через терминал:

:::tabs
== Отобразить

Чтобы отобразить процент заряда батареи, введите соответствующую команду в терминале:

```shell
gsettings set org.gnome.desktop.interface show-battery-percentage true
```

== Скрыть

Чтобы скрыть процент заряда батареи, введите соответствующую команду в терминале:

```shell
gsettings set org.gnome.desktop.interface show-battery-percentage false
```

:::

### Как определить какой тип сессии используется: X11 или Wayland?

Для определения типа текущей сессии пользователя в рабочем окружении GNOME, существует несколько вариантов:

:::tabs
== Глобальная переменная окружения
Получить значение глобальной переменной окружения `XDG_SESSION_TYPE`, введите в терминале:

```shell
echo $XDG_SESSION_TYPE
```

:::details Пример вывода команды:

```shell
[oleg@alt-gnome ~]$ echo $XDG_SESSION_TYPE
wayland
```

== inxi

Используйте утилиту `inxi` с опцией `-G`:

```shell
inxi -G
```

:::details Пример вывода команды:

```shell
Graphics:
  Device-1: Advanced Micro Devices [AMD/ATI] Phoenix3 driver: amdgpu v: kernel
  Device-2: IMC Networks Integrated Camera driver: uvcvideo type: USB
  Display: wayland server: X.org v: 1.21.1.15 with: Xwayland v: 24.1.4
    compositor: gnome-shell v: 47.3 driver: X: loaded: amdgpu
    unloaded: fbdev,modesetting,radeon,vesa dri: radeonsi gpu: amdgpu
    resolution: 1920x1200~60Hz
  API: EGL v: 1.5 drivers: kms_swrast,radeonsi,swrast
    platforms: gbm,wayland,x11,surfaceless,device
  API: OpenGL v: 4.6 compat-v: 4.5 vendor: amd mesa v: 24.3.3 renderer: AMD
    Radeon Graphics (radeonsi gfx1103_r1 LLVM 18.1.8 DRM 3.59
    6.12.9-6.12-alt1)
  API: Vulkan v: 1.3.296 drivers: N/A surfaces: xcb,xlib,wayland
  Info: Tools: api: clinfo, eglinfo, glxinfo, vulkaninfo wl: wayland-info
    x11: xdpyinfo, xprop, xrandr
```

== Настройки
![Подробности о системе](/quick-start/quick-start-1.png 'В рабочем окружении GNOME перейдите в Настройки -> Система -> Подробности о системе')
:::

::: info
После авторизации вы сможете узнать значение текущей сессии. Если вы вошли в систему (сессию) как суперпользователь (root), то информация о типе сессии будет недоступна.
:::

## Сетевое администрирование

### Как узнать какие стандарты Wi-Fi поддерживает модуль?

Чтобы узнать, какие стандарты Wi-Fi поддерживает ваш модуль в ALT Regular Gnome, введите в терминале:

```shell
lspci | egrep -i --color 'wifi|wlan|wireless'
```

| Стандарт | Альтернативное обозначение | Год выпуска |
| -------- | -------------------------- | ----------- |
| 802.11n  | Wi-Fi 4                    | 2009        |
| 802.11ac | Wi-Fi 5                    | 2013        |
| 802.11ax | Wi-Fi 6                    | 2019        |

:::details Пример вывода команды

```shell
02:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8852BE PCIe 802.11ax Wireless Network Controller
```

:::
