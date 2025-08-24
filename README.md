# 🚀 Руководство по развертыванию мониторинга

## 📋 Шаги для развертывания

### 1️⃣ Развертывание стека

```bash
git clone repo
docker swarm init
docker stack deploy -c docker-compose.yml monitoring
```

### 2️⃣ Добавление источника данных в Grafana

Добавьте источник данных **Prometheus** в Grafana с адресом:

```
http://prometheus:9090
```

### 3️⃣ Настройка конфигурации Prometheus

Добавьте следующие строки в конец файла:
```
/var/lib/docker/volumes/monitoring_prom-configs/_data/prometheus.yml
```

В секцию `scrape_configs`:

```yaml
- job_name: 'node-exporter'
  static_configs:
    - targets: ['node-exporter:9100']
```

### 4️⃣ Перезагрузка конфигурации Prometheus

```bash
docker ps | grep prometheus | awk '{print $1}' | xargs docker kill -s SIGHUP
```

### 5️⃣ Импорт дашборда в Grafana

Импортируйте дашборд по ссылке:

🔗 [https://grafana.com/grafana/dashboards/1860](https://grafana.com/grafana/dashboards/1860)

---

## ✅ Готово!

После выполнения всех шагов ваш стек мониторинга будет готов к работе.
