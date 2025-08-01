# Jenkins in Docker Setup Guide
## Prerequisites

Make sure you have the following installed:

- [Docker](https://www.docker.com/products/docker-desktop/)
- Internet connection (to pull the Jenkins image)

Check Docker version:

```bash
docker --version
```
<img width="930" height="245" alt="Screenshot from 2025-08-01 13-39-22" src="https://github.com/user-attachments/assets/c7b2665a-c977-441f-a6f5-b1faa4b30988" />

---

## Create Docker Volume

To persist Jenkins data across container restarts:

```bash

docker volume create jenkins-data
```
<img width="701" height="57" alt="Screenshot from 2025-08-01 13-43-43" src="https://github.com/user-attachments/assets/204b4d9f-5417-451b-bee4-000e8dd10f10" />

---

##  Run Jenkins Container

Run the official Jenkins LTS image with persistent storage and port mapping:

```bash

docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins-data:/var/jenkins_home \
  jenkins/jenkins:lts-jdk17
```
<img width="701" height="57" alt="Screenshot from 2025-08-01 13-43-43" src="https://github.com/user-attachments/assets/15064bc7-421e-4c31-9460-2529f38f0f8c" />

---

## Get Jenkins Initial Admin Password
To unlock Jenkins for first-time setup:

```bash

docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

```
<img width="1037" height="65" alt="Screenshot from 2025-08-01 13-52-10" src="https://github.com/user-attachments/assets/81930c8c-fbb1-41f7-b4aa-01e8ba15f894" />



<img width="1788" height="967" alt="Screenshot from 2025-08-01 13-15-24" src="https://github.com/user-attachments/assets/d92d790f-e924-4d43-bce3-331ef8d51d6e" />

---
## Customize jenkins
<img width="1788" height="967" alt="Screenshot from 2025-08-01 13-15-51" src="https://github.com/user-attachments/assets/f0478e65-81ef-4111-a5b4-cee033040e82" />

<img width="1788" height="967" alt="Screenshot from 2025-08-01 13-16-56" src="https://github.com/user-attachments/assets/ea07b983-b98f-494d-b3d8-8d19bee99546" />



---
## creating an admin user

<img width="1788" height="967" alt="Screenshot from 2025-08-01 13-18-21" src="https://github.com/user-attachments/assets/9ee40795-11ae-45ea-ad99-2e5584731904" />

---


## Access Jenkins UI

Open your browser and visit:

```bash 
http://localhost:8080
```
<img width="1788" height="967" alt="Screenshot from 2025-08-01 13-19-24" src="https://github.com/user-attachments/assets/21b5201e-c667-4645-a77f-417c0a591b15" />

## Jenkins Dashboard 

<img width="1846" height="968" alt="Screenshot from 2025-08-01 13-19-55" src="https://github.com/user-attachments/assets/a7b2b1da-8b72-4f0d-82a6-767ad3e8ac95" />

---

 ## References
``
    Official Jenkins Docker Hub 
   ( https://hub.docker.com/r/jenkins/jenkins/)
    Jenkins Documentation

    
