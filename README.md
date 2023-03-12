# REF
- [https://github.com/docker/awesome-compose/blob/master/plex/compose.yaml](https://github.com/docker/awesome-compose/blob/master/plex/compose.yaml)

# Wakatime 

- [https://wakatime.com/@spcn21/projects/pszcfeeact](https://wakatime.com/@spcn21/projects/pszcfeeact)

ขั้นตอนการติดตั้งอยู่ใน swarm01 ก่อนถึงการสร้าง images เข้า dockerhub

- [https://github.com/SiwakornEDZ/swarm01/edit/master/README.md](https://github.com/SiwakornEDZ/swarm01/edit/master/README.md)

# URL (plex)

- [plex888.xops.ipv9.me](plex888.xops.ipv9.me)


### กำหนดค่าไฟล์ compose.yaml เพื่อนำไป deploy stack ใน portainer

```
version: '3.3'
services:
  plex:
    image: siwakorn2345/plex:sw06
    networks:
     - webproxy
    logging:
      driver: json-file
    deploy:
      replicas: 1
      labels:
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.plex888-https.entrypoints=websecure
        - traefik.http.routers.plex888-https.rule=Host("plex888.xops.ipv9.me")
        - traefik.http.routers.plex888-https.tls.certresolver=default
        - traefik.http.services.plex888.loadbalancer.server.port=32400
      resources:
        reservations:
          cpus: '0.1'
          memory: 6M
        limits:
          cpus: '0.4'
          memory: 250M
networks:
  webproxy:
    external: true
```
    
### อธิบาย Docker Compose file

- [Docker Compose]

# Ref example code 

- https://github.com/pitimon/dockerswarm-inhoure?fbclid=IwAR05dUk05KjPAWSfDZs0ecF9RjuXh6w86rTt2IFKUQrwSrFopYEgTj-x6dY
