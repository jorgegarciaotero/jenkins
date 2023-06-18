## JENKINS

### 1. Instalación Jenkins en Docker:
- __1.1. Instalación Jenkins__: ```docker pull jenkinsci/jenkins```
  - __Comprobación imagen:__ ```docker images```
  - __Docker Compose:__: definición de un archivo de Docker para levantar el servicio Jenkins ```docker-compose.yaml```
        ```
        version: '3'
        services:
        jenkins:                #Define el servicio de jenkins
            container_name: jenkins      #imagen que usa como plantilla
            image: jenkins/jenkins
            build:
            context: jenkins_ansible
            ports:
            - '8081:8080'               #puerto navegador
            volumes:
            - $PWD/jenkins_home:/var/jenkins_home  #Datos que queremos que sobrevivan
            networks:
            - net
        remote_host:
            image: remote_host
            build:
            context: centos7
            networks:
            - net
        db_host:
            container_name: db
            image: mysql:5.7
            environment:
            - "MYSQL_ROOT_PASSWORD=fakepassword"
            volumes:
            - $PWD/db_data:/var/lib/mysql
            networks:
            - net
        networks:
            net:
        ```
    
    - __Montar la imagen:__: Con ```docker-compose up -d``` leemos el docker-compose.yaml. Montamos la imagen de docker-compose con todos los servicios.
      - Con ```docker ps`` vemos el contenedor:
        ``` 
        jorge@vweb-1:~/jenkins$ docker ps
        CONTAINER ID   IMAGE             COMMAND                  CREATED        STATUS          PORTS                                                  NAMES
        2c3d6b70306c   jenkins/jenkins   "/usr/bin/tini -- /u…"   15 hours ago   Up 30 minutes   50000/tcp, 0.0.0.0:8081->8080/tcp, :::8081->8080/tcp   jenkins
        ```




# jenkins
