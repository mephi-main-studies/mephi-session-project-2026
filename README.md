### Отчёт по выполнению задания

Ниже - таблица строго в формате задания, дополненная столбцами «Раздел» и «Как получено / Подтверждение».

#### Таблица артефактов и подтверждений

| Файл | Раздел | Что проверяется | Как получено / Подтверждение                                                                                                                   |
|---|---:|---|------------------------------------------------------------------------------------------------------------------------------------------------|
| `mephi-screenshot.png` | 7, 8 | Визуальное подтверждение | В терминале выполнено `curl http://localhost/` с ответом `Hello from Student: M265813`; сделан скриншот и сохранён как `mephi-screenshot.png`. |
| `history.out` | 2, 3, 4, 5, 6, 7, 8 | Выполненные команды | Сохранено командой `history > ~/history.out` (см. строку 66 в `history.out`).                                                                  |
| `ping.out` | 1 | Работоспособность сети | `ping -c 4 8.8.8.8 > ~/ping.out` - в файле 4 ответа, 0% потерь.                                                                                |
| `dnf.out` | 2 | Управление пакетами | `dnf history list > ~/dnf.out` - видно `dnf -y upgrade --refresh` и установку `nginx libcap-ng-utils`.                                         |
| `stat.out` | 3, 5, 8 | Установка прав доступа и контекста SELinux | `stat /data/mephi-2026 > ~/stat.out; stat /mephi-web >> ~/stat.out`. Для `/mephi-web` контекст `httpd_sys_content_t` подтверждён.              |
| `journalctl.out` | 4 | Запуск веб-сервера | `journalctl -u nginx.service -b > ~/journalctl.out` - логи текущей загрузки с запуском nginx и проверкой конфигурации.                         |
| `getcap.out` | 5.2 | Настройка привилегий | `getcap /usr/sbin/tcpdump > ~/getcap.out` - в файле: `cap_net_admin,cap_net_raw=eip`.                                                          |
| `getenforce.out` | 5.3 | Режим SELinux | `getenforce > ~/getenforce.out` - значение `Enforcing`.                                                                                        |
| `curl.out` | 7, 8 | Результат тестирования | `curl http://localhost/ > ~/curl.out` - содержит `Hello from Student: M265813`.                                                                |
| `fstab` | 3 | Настройка монтирования файловых систем | Сохранён плоским именем `fstab`; содержит `LABEL=MEPHI_WEB  /mephi-web  ext4  defaults  0 0`.                                                  |
| `passwd` | 5.1 | Управление пользователями | Сохранён плоским именем `passwd`; присутствуют пользователи `user1` (5501), `user2` (5502), `user3` (5503), `curator1`, `curator2`.            |
| `shadow` | 6.2 | Управление паролями пользователей | Сохранён плоским именем `shadow`; для пользователей установлен срок смены пароля `max=90` (команды `chage -M 90 ...`).                         |
| `group` | 5.1 | Управление группами пользователей | Сохранён плоским именем `group`; есть `curators:x:4444:` и `mephi-team:x:4445:user1,user2,user3`.                                              |
| `pwquality.conf` | 6.2 | Настройка пароля | Сохранён плоским именем `pwquality.conf`; параметр `minlen = 12`.                                                                              |

#### Дополнительно (артефакты, усиливающие проверяемость)
- `hostnamectl.out` (раздел 1): подтверждает FQDN `mephi-2026.domain.local`.
- `nmcli_device_status.out`, `nmcli_conn_activate.out` (раздел 1): подтверждают активность интерфейса/подключения.
- `pam_login.out`, `access_conf.out` (раздел 6.1): подтверждают запрет локального входа для группы `curators` через `pam_access.so`. 
