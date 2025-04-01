# Prometheus monitoring on vm

### Задача
1) Определить метрики для сайта bank.yandex.ru
2) Развернуть Prometheus
3) Настроить пробы по выбранным метрикам

### Решение
1) В качестве метрик выбраны HTTP запросы 200OK, 301 и 302. Поскольку реддиректы считаем за успешную работу сайта
2) Сделаем исталляцию docker compose:
```shell
#!/bin/bash (либо через файл)

apt-get remove docker docker-engine docker.io containerd runc
apt-get install ca-certificates curl gnupg lsb-release
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Развернем prometheus с blackbox (позволит собирать пробы HTTP с сайта)
```shell
docker compose down -v #Удалим предыдущее состояние
docker compose up -docker #Развернем новое
```

