# thoughtworkstest

Steps to perform the test
1. Created an ec2-instance on aws
2. Allocate and Associate elastic ip to ec2-instance
2. Installed Docker and enabled it
3. create Dockerfile (attached) 
4. Build the docker image (thoughtworks:1)

   ```docker image build -t thoughtworks:1 .```
5. Created Docker container(mediawiki) using the above image and did port mapping 

    ```docker container run -d --name mediawiki -p 8080:80 thoughtworks:1```
    
6. create common docker network mediawiki
   ```docker network create mediawiki```

7. Attach the container to mediawiki network
    ```docker network connect mediawiki mediawiki```

8. create Docker container for Mysql and configure, Also joined the same container with the same network created in step 6 . (As in requested it was mentioned it needs to be created on separate VM
```
   docker run -d --name mediawiki-mysql \
  --env ALLOW_EMPTY_PASSWORD=yes \
  --env MARIADB_USER=manojpathak \
  --env MARIADB_PASSWORD=Password@148 \
  --env MARIADB_DATABASE=my_wiki \
  --network mediawiki  \
  --volume mediawiki-mysql:/var/lib/mysql \
   bitnami/mariadb:latest
   ```
9. Confirm both the container connected to same network 
   ```
   docker network connect mediawiki mediawiki
   docker network connect mediawiki mediawiki-mysql
   
   ```
9. Took outthe ip of database container mediawiki-mysql from ```docker container inspect <id>``` command
10. Hit the public ip of AWS ec2-instance witht port number 
   #http://34.198.38.111:8080/
11. Provided private ip of database container while doing database installation on mediawiki
12. configure it and download localsettip.php

  
 
