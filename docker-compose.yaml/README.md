# Docker Compose ไฟล์นี้มีการกำหนดการใช้งาน Docker container สำหรับ Plex Media Server ดังนี้:

* image: linuxserver/plex: กำหนด image ของ Docker container จาก repository linuxserver/plex ซึ่งเป็น image ที่มีการตั้งค่าพร้อมใช้งานสำหรับ Plex Media Server
* container_name: plex: กำหนดชื่อของ container เป็น plex
* network_mode: host: กำหนดให้ container ใช้ network mode host ซึ่งจะใช้ network stack ของ host machine โดยตรง จึงจะสามารถใช้ IP ของ host machine ได้โดยไม่ต้องเปลี่ยนแปลงการกำหนด network settings ของ container
* environment: - VERSION=docker: กำหนด environment variable ให้ container โดยกำหนดค่า VERSION เป็น docker เพื่อบอกให้ Plex Media Server รู้ว่าจะใช้ version ไหนสำหรับ Docker
* restart: always: กำหนดให้ container restart โดยอัตโนมัติเมื่อมีการเริ่มต้น Docker daemon ใหม่หรือ container หยุดทำงาน
* volumes: - ${PLEX_MEDIA_PATH}:/media/: กำหนดการ mount volume จาก host machine ไปยัง container โดยกำหนดให้ path ของ volume บน host machine เป็น ${PLEX_MEDIA_PATH} และ path ของ volume ใน container เป็น /media/ ซึ่งเป็นที่เก็บไฟล์ media ของ Plex Media Server ใน container นี้

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

## docker depoly

```
sudo docker compose up -d
```

### กำหนด tag ของ images ที่ต้องการ

```
docker tag linuxserver/plex:lastest siwakorn2345/plex:sw06
```
 
### push images ขึ้น docker hub และเพื่อเรียกใช้้งานใน dockercompose file

```
docker push siwakorn2345/plex:sw06
```

