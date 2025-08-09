# 📊 Grafana + Prometheus + Node Exporter (Docker Compose)

Полный стек мониторинга на **Ubuntu 22.04**.

---

## 🚀 Установка

### 1. Установите Docker и Docker Compose
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io docker-compose -y
sudo systemctl enable docker
sudo systemctl start docker

````

---

### 2. Клонируйте проект или создайте папку

```bash
mkdir ~/grafana-prometheus && cd ~/grafana-prometheus
```

---

### 3. Конфигурация Prometheus

**`prometheus.yml`**:

```yaml
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['prometheus:9090']

  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']
```

---

### 4. Docker Compose файл

**`docker-compose.yml`**:

```yaml
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
    volumes:
      - grafana-data:/var/lib/grafana
    restart: unless-stopped

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
      - "9100:9100"
    restart: unless-stopped

volumes:
  grafana-data:
```

---

### 5. Запуск

```bash
docker-compose up -d
```

---

## 🔍 Доступ

* **Prometheus** → [http://localhost:9090](http://localhost:9090)
* **Grafana** → [http://localhost:3000](http://localhost:3000)

  * Логин: `admin`
  * Пароль: `admin` (измените при первом входе)
* **Node Exporter** → [http://localhost:9100/metrics](http://localhost:9100/metrics)

---

## 📈 Настройка Grafana

1. Войдите в Grafana.
2. Перейдите в **Connections → Data Sources → Add data source**.
3. Выберите **Prometheus**.
4. Укажите `http://prometheus:9090`.
5. Сохраните.
6. Импортируйте дашборд с ID `1860` для Node Exporter.

---

## 🛑 Остановка

```bash
docker-compose down
```

## 🔄 Перезапуск

```bash
docker-compose restart
```

---

## 📦 Структура проекта

```
grafana-prometheus/
│── docker-compose.yml
│── prometheus.yml
└── README.md
```
📜 Лицензия
MIT License — используйте и модифицируйте свободно.
