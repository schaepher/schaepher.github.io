---
title: jfrog-artifactory
date: 2019-10-09 14:46:33
updated: 2019-10-09 14:46:33
tags:
---

Pro 破解：  
https://ciphers.pw/resources/artifactory-pro-license-crack-6-6-0.119/

```
java -jar artifactory-injector-1.1.jar
```

先选 2，注入到目录：`/opt/jfrog/artifactory`  
再选 1，得到 license  

然后访问 web，输入账号密码。  

用户名：admin  
密码：password

会提示没有 license，按提示点进去，把刚刚生成的 license 放进去就行了。

问题：  Timed out waiting for join.key file to be made available at /var/opt/jfrog/artifactory/etc/security/join.key   
解决：  

```
# Upload the access.war and artifactory.war via the Tomcat Manager webapp.
# As soon as these are uploaded, stop tomcat and delete the automatically-created artifactory folder.

# Create artifactory folder.
mkdir /usr/share/artifactory
chown tomcat.tomcat /usr/share/artifactory
cd /usr/share/artifactory

# Start tomcat.
service tomcat8 start

# Monitor the etc/security folder repeatedly until it has been automatically created by the artifactory webapp (a few seconds):
ls etc/security
ls etc/security
ls etc/security

# Create a new master key for artifactory:
openssl rand -hex 16 > etc/security/master.key
chown tomcat.tomcat etc/security/master.key
chmod 600 etc/security/master.key

# Monitor the access/etc/keys folder repeatedly until it has been automatically created by the access webapp  (about 20 seconds):
ls access/etc/keys
ls access/etc/keys
ls access/etc/keys

# Create a new join key for access:
openssl rand -hex 16 > access/etc/keys/join.key
chown tomcat.tomcat access/etc/keys/join.key
chmod 600 access/etc/keys/join.key
cp -a access/etc/keys/join.key etc/security/join.key

# Check the logs to confirm artifactory was able to connect to the access server:
tail logs/artifactory.log

2019-06-03 15:47:51,644 [art-init] [INFO ] (o.a.w.s.ArtifactoryContextConfigListener:215) -
###########################################################
### Artifactory successfully started (53.527 seconds)   ###
###########################################################
```

参考链接：  
https://stackoverflow.com/questions/55142890/join-key-file-not-created-or-deleted-on-upgrade-to-6-8-x-artifactory-pro/56430896#56430896


docker-compose.yml  

```
version: '2'
services:
  postgresql:
    image: docker.bintray.io/postgres:9.6.11
    container_name: postgresql
    ports:
     - 5432:5432
    environment:
     - POSTGRES_DB=artifactory
     # The following must match the DB_USER and DB_PASSWORD values passed to Artifactory
     - POSTGRES_USER=jfrog
     - POSTGRES_PASSWORD=9f2X3Bg3ZeEMINlgTgrx
    volumes:
     - postgresql:/var/lib/postgresql/data
    restart: always
    ulimits:
      nproc: 65535
      nofile:
        soft: 32000
        hard: 40000
  artifactory:
    image: docker.bintray.io/jfrog/artifactory-pro:6.13.1
    container_name: artifactory
    ports:
     - 9003:8081
    depends_on:
     - postgresql
    links:
     - postgresql
    volumes:
     - artifactory:/var/opt/jfrog/artifactory
    environment:
     - DB_TYPE=postgresql
     # The following must match the POSTGRES_USER and POSTGRES_PASSWORD values passed to PostgreSQL
     - DB_USER=jfrog
     - DB_PASSWORD=9f2X3Bg3ZeEMINlgTgrx
     # Add extra Java options by uncommenting the following line
     - EXTRA_JAVA_OPTIONS=-Xms512m -Xmx4g
    restart: always
    ulimits:
      nproc: 65535
      nofile:
        soft: 32000
        hard: 40000

volumes:
    artifactory:
    postgresql:
```


1. 要先注入，否则无法启动。注入后会自动重启。注入后要立即让工具生成 License
2. 启动期间要生成 join key  
   会有提示：  
   ```
   join.key not found, waiting for sync
   ```
  
openssl rand -hex 16 > etc/security/master.key
chown tomcat.tomcat etc/security/master.key
chmod 600 etc/security/master.key

openssl rand -hex 16 > access/etc/keys/join.key
chown tomcat.tomcat access/etc/keys/join.key
chmod 600 access/etc/keys/join.key
cp -a access/etc/keys/join.key etc/security/join.key