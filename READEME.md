# 資料結構
```
leodock
├── docker-compose.yml
├── logs
├── apache2
│   ├── apache2.conf
│   └── sites
│       └── sample.conf.example
├── mysql
│   ├── Dockerfile
│   └── my.cnf
└── php
    ├── Dockerfile
    ├── php.ini
    └── vhost.conf
```

# 設定環境

```
cp .env.example .env

cp apache2/ports.conf.example apache2/ports.conf
```

# 啟動
```
docker-compose up -d 
```