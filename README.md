# MongoDB ReplicaSet Using Docker



### 1. 도커로 MongoDB 3대 생성
- docker network create mongoCluster        // 미리 생성 시, docker-compose.yml >  external: true 설정
```bash
> docker-compose up -d
```

### 2. 호스트 설정
```bash
> sudo vi /etc/hosts

// 호스트 추가
127.0.0.1   mongo1
127.0.0.1   mongo2
127.0.0.1   mongo3
```

### 3. replica 설정

```bash
> docker exec -it ${containerId} mongosh

> rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "mongo1:27017" },
    { _id: 1, host: "mongo2:27018" },
    { _id: 2, host: "mongo3:27019" }
  ]
})

> rs.status()       // primary, secondary 확인
```

4. 접속
```bash
mongodb://127.0.0.1:27017,127.0.0.1:27018,127.0.0.1:27019/db?replicaSet=rs0
```

