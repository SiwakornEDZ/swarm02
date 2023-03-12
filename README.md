# REF
- [https://github.com/docker/awesome-compose/blob/master/plex/compose.yaml](https://github.com/docker/awesome-compose/blob/master/plex/compose.yaml)

ขั้นตอนการติดตั้งอยู่ใน swarm01 ก่อนถึงการสร้าง images เข้า dockerhub

- [https://github.com/SiwakornEDZ/swarm01/edit/master/README.md](https://github.com/SiwakornEDZ/swarm01/edit/master/README.md)

# URL (plex)

- [plex888.xops.ipv9.me](plex888.xops.ipv9.me)

## สร้าง image สำหรับการเตรียม push ขึ้น dockerhub

### ขั้นตอนแรก

### ตรวจเช็ค image ใน docker โดยใช้คำสั่ง

```
docker images
```

### ขั้นตอนที่ 2

### login docker โดยใช้  username และ password

```
docker login
```
### ขั้นตอนที่ 3 

### กำหนด tag ของ images ที่ต้องการ

```
docker tag swarm02-web siwakorn2345/swarm02-web:01
```
 
### psuh images ขึ้น docker hub และเพื่อเรียกใช้้งานใน dockercompose file

```
docker push siwakorn2345/swarm02-web:01
```

### กำหนดค่าไฟล์ compose.yaml เพื่อนำไป deploy stack ใน portainer
## ยังไม่สมบูรณ์

```
version: '3.3'
services:
  test-volume:
    image: siwakorn2345/swarm01-backend:01
    networks:
     - webproxy
    logging:
      driver: json-file
    deploy:
      replicas: 1
      labels:
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.whale0011-https.entrypoints=websecure
        - traefik.http.routers.whale0011-https.rule=Host("whale0011.xops.ipv9.me")
        - traefik.http.routers.whale0011-https.tls.certresolver=default
        - traefik.http.services.whale0011.loadbalancer.server.port=80
      resources:
        reservations:
          cpus: '0.1'
          memory: 6M
        limits:
          cpus: '0.4'
          memory: 50M
networks:
  webproxy:
    external: true
```
    
## ยังไม่สมบูรณ์

# Ref example code 

- https://github.com/pitimon/dockerswarm-inhoure?fbclid=IwAR05dUk05KjPAWSfDZs0ecF9RjuXh6w86rTt2IFKUQrwSrFopYEgTj-x6dY
