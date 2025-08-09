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
