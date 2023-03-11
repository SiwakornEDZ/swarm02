# REF 
- [https://github.com/docker/awesome-compose/tree/master/plex](https://github.com/docker/awesome-compose/tree/master/plex)
- https://wakatime.com/@spcn21/projects/pszcfeeact

ขั้นตอนการติดตั้งอยู่ใน swarm01 ก่อนถึงการสร้าง images เข้า dockerhub

- [https://github.com/SiwakornEDZ/swarm01/edit/master/README.md](https://github.com/SiwakornEDZ/swarm01/edit/master/README.md)

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
 version: '3.7'
 services:
  web:
    image: siwakorn2345/swarm01-backend:02
    command: --providers.docker --entrypoints.web.address=:90 --providers.docker.exposedbydefault=false
    networks:
      - webproxy
     environment:
      - PORT=80
    volumes:
      - appwhale189:/usr/src/app/appwhale889
    ports:
      - "91:90"
    depends_on:
      - deploy
    deploy:
      replicas: 1
      labels:
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.${appname}-https.entrypoints=websecure
        - traefik.http.routers.${appname}-https.rule=Host("{appname}.xops.ipv9.me")
        - traefik.http.routers.${appname}-https.tls.certresolver=default
        - traefik.http.services.${appname}.loadbalancer.server.port=80
        - "traefik.http.routers.go.rule=Path(`/`)"
        - "traefik.http.services.go.loadbalancer.server.port=80"
      restart_policy:
        condition: any
      update_config:
        delay: 5s
        parallelism: 1
        order: start-first
volumes:
  appwhale189:

networks:
  default:
    driver: overlay
    attachable: true   
  webproxy:
    external: true
```
    
## ยังไม่สมบูรณ์

# Ref example code 

- https://github.com/pitimon/dockerswarm-inhoure?fbclid=IwAR05dUk05KjPAWSfDZs0ecF9RjuXh6w86rTt2IFKUQrwSrFopYEgTj-x6dY
