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

### 2. Клонируйте репозиторий
```bash
git clone https://github.com/username/grafana-prometheus-monitoring.git
cd grafana-prometheus-monitoring

### 3. Структура проекта
.
├── docker-compose.yml
├── prometheus
│   └── prometheus.yml
└── README.md

📄 Конфигурация
docker-compose.yml
version: "3.8"
```yaml
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    volumes:
      - ./prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
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
    volumes:
      - grafana-data:/var/lib/grafana
    restart: unless-stopped

volumes:
  grafana-data:

prometheus/prometheus.yml
```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["prometheus:9090"]

  - job_name: "node-exporter"
    static_configs:
      - targets: ["node-exporter:9100"]

▶️ Запуск
```bash
docker-compose up -d
Проверка контейнеров:
```bash
docker ps

🌐 Доступ к сервисам
Prometheus → http://localhost:9090

Node Exporter → http://localhost:9100/metrics

Grafana → http://localhost:3000
Логин: admin
Пароль: admin (попросит сменить при первом входе)

📊 Настройка Grafana
Зайдите в Grafana.

Добавьте источник данных:
URL: http://prometheus:9090
Импортируйте готовые дашборды, например:
Node Exporter Full (ID: 1860)
Prometheus Stats (ID: 2)

🛑 Остановка и удаление
```bash
docker-compose down

📌 Полезное
Документация Grafana
Документация Prometheus
Node Exporter GitHub

```yaml
---
Хочешь, я тебе ещё сразу сделаю готовую **структуру файлов с этим README и конфигами**, чтобы можно было просто `git clone && docker-compose up -d` и всё заработало?  
Тогда вообще будет под ключ.
