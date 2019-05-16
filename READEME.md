# 資料結構
```
leodock
├── docker-compose.yml
├── logs
├── apache2
│   ├── apache2.conf
│   └── sites
│       └── sample.conf.example
└── php
    ├── Dockerfile
    ├── php.ini
    └── vhost.conf
```

# 設定環境

```
cp .env.example .env

```

# 啟動
```
docker-compose up -d 
```

# 備註

可搭配 leodock 一起使用

此 docker 不包含 mysql

mysql 需要連線到 leodock