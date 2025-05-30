
# InfluxDB, Telegraf и Grafana в Docker

Этот Docker-комплекс разворачивает полностью интегрированную связку InfluxDB, Telegraf и Grafana, объединяя все сервисы единым токеном. В комплект входят две демонстрационные дашборды для примера.
По сути, это готовая система для сбора данных с любых датчиков или любых источников данных.

## Настройка

Если вам нужны специфические настройки безопасности, переименуйте файл `.env.example` в `.env` и заполните его.

### Инициализация InfluxDB

1. Для первичной инициализации базы данных InfluxDB выполните:
   ```bash
   docker compose up influxdb_cli
   ```
   После инициализации (через 10–15 секунд) нажмите `Ctrl + C`.

2. Запустите все сервисы:
   ```bash
   docker compose up -d
   ```

3. Остановите все сервисы:
   ```bash
   docker compose down
   ```

### Запуск только Grafana

```bash
docker compose up -f docker-compose-only-grafana.yml -d
```

### Структура папок

- `telegraf/telegraf-conf/` – конфигурация Telegraf
  - `telegraf.conf` – содержит настроенный output в InfluxDB.
  - `telegraf.d/` – папка с конфигурациями input для различных источников данных.
- `telegraf/mibs/` – MIB-файлы для опроса SNMP-устройств (заменяет `/usr/share/snmp/mibs`).

### Сервисы

- Grafana: http://localhost:3000  
  Логин/пароль: admin / admingrafana

- InfluxDB: http://localhost:8086  
  Логин/пароль: admin / admininflux

## Важно

Токены и пароли заданы заранее – это установка для обучения и знакомства с технологиями.

Рекомендуется:
- Создайте новый токен в интерфейсе InfluxDB.
- Вставьте этот токен в файл конфигурации `telegraf.conf`.
- Добавьте новый источник данных в Grafana, используя этот токен.
- Наконец, смените пароли для интерфейсов InfluxDB и Grafana на уникальные и безопасные.

### Конфигурация

- Grafana: Настраивается через переменные окружения в `docker-compose.yml`.
- InfluxDB: Данные хранятся в папке `influxdb2` и настраиваются через переменные окружения в `docker-compose.yml`.
- Telegraf: Настройки указаны в `telegraf/telegraf.conf`.

### Сеть и Тома

- Сеть: lab240-monitoring
- Тома:
  - grafana-data: данные Grafana
  - ./influxdb2: данные InfluxDB