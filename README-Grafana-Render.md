# Grafana Render

## .env:
```
cp env-default .env
vim .env

>>>

# 使用插件，第一次 up 安裝後可以留空，省時不再重安裝
GRAFANA_PLUGINS=grafana-image-renderer

# 搭配 docker-compose.yml 對內部 3000 port
GRAFANA_RENDERING_CALLBACK_URL=http://grafana:3000/

# 可開此 port 用此進行測試
GRAFANA_RENDER_PORT=8099
```


## docker-compose.yml
```
vim docker.compose.yml

>>>

# 取代原有 network yml 語法，至已建立之 docker network：
networks:
  default:
    external:
      name: xxx
  frontend:
    external:
      name: xxx
  backend:
    external:
      name: xxx
```

## Up
```
docker-compose up -d grafana-render
```

## Browser Grafana

1. http://172.31.251.104:3001
0. 創建 MySQL 連線，路徑: Configuration > Data Sources。  請命名 Name: MYSQL_TW_APPLICATION，寫入 prtg 專案之 .env > GRAFANA_DB_NAME=MYSQL_TW_APPLICATION
0. 創建 Token，路徑: Configuration > API Keys

Role     | Requirement
---------|--------------------------------------------------------------
Admin    | (最後的"等號"記得複製) 貼進 prtg 專案之 .env > GRAFANA_TOKEN_ADMIN=
Viewer   | 貼進 prtg 專案之 .env > GRAFANA_TOKEN_VIEWER=

