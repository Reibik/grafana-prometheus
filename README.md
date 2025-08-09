````markdown
# 📊 Мониторинг сервера с Grafana + Prometheus + Node Exporter

Этот проект поднимает систему мониторинга на базе **Grafana**, **Prometheus** и **Node Exporter** в Docker.  
Подходит для мониторинга Linux-серверов с визуализацией метрик.

---

## 📦 Что входит
- **Prometheus** — сбор и хранение метрик
- **Node Exporter** — экспорт системных метрик сервера
- **Grafana** — веб-интерфейс для визуализации данных

---

## 🚀 Установка и запуск

### 1. Установите Docker и Docker Compose
```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl enable --now docker
````

### 2. Клонируйте проект

```bash
git clone https://github.com/USERNAME/grafana-prometheus-monitoring.git
cd grafana-prometheus-monitoring
```

### 3. Структура проекта

```
grafana-prometheus-monitoring/
│── docker-compose.yml
│── prometheus.yml
└── README.md
```

---

## ⚙️ Конфигурация Prometheus (`prometheus.yml`)

```yaml
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["prometheus:9090"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["node-exporter:9100"]
```

---

## 📜 docker-compose.yml

```yaml
version: "3.8"

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
    restart: unless-stopped

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
      - "9100:9100"
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
    restart: unless-stopped
```

---

## ▶️ Запуск

```bash
docker-compose up -d
```

---

## 🔗 Доступ

* **Prometheus:** http\://SERVER\_IP:9090
* **Node Exporter:** http\://SERVER\_IP:9100/metrics
* **Grafana:** http\://SERVER\_IP:3000 (логин: `admin`, пароль: `admin`)

---

## 📊 Настройка Grafana

1. Перейдите в Grafana → **Configuration → Data Sources**
2. Добавьте **Prometheus** с URL:

   ```
   http://prometheus:9090
   ```
3. Импортируйте готовый **Dashboard**:

   * ID: `1860` (Node Exporter Full)
   * Источник: [Grafana Dashboards](https://grafana.com/grafana/dashboards/1860)

---

## 🛑 Остановка

```bash
docker-compose down
```

---

## 📜 Лицензия

MIT License — используйте и модифицируйте свободно.

```

---

Хочешь, я тебе к этому `README.md` сразу сделаю полный рабочий **архив с docker-compose.yml и prometheus.yml**, чтобы можно было скачать и запустить без правок?  
Тогда будет реально "под ключ".
```
