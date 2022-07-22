## 常用服务搭建

### redis

```
docker pull redis:5.0

docker run -itd --name redis -p 6379:6379 redis:5.0
```

### MongoDB

```
docker run --name mongo -v /data/mongo:/data/db -p 27017:27017 -d mongo:5.0 --auth
docker exec -it mongo mongo admin
db.createUser({ user: 'root', pwd: '123456', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
```

### Postgresql

```
# 默认用户名：postgres
docker pull postgres:13.5
docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:13.5
docker exec -it postgres /bin/bash
psql -U postgres -W 123456
```

### Elasticsearch

#### elasticsearch

```
docker pull elasticsearch:6.8.23
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:6.8.23
./elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.8.23/elasticsearch-analysis-ik-6.8.23.zip
exit
docker restart elasticsearch
```

#### elasticsearch-kibana

```
docker pull nshou/elasticsearch-kibana
docker run -it --name es-kibana -d -p 9200:9200 -p 5601:5601 nshou/elasticsearch-kibana

docker exec -it es-kibana /bin/bash
cd /home/elasticsearch/elasticsearch-7.16.2/bin
./elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.16.2/elasticsearch-analysis-ik-7.16.2.zip
exit
docker restart es-kibana
```

#### 