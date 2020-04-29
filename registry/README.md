# Configure your Local Registry:

first thing guys if you want to upload your customize image to docker registry 
1. first you have to make docker hub id through hub.docker.com...done

Docker by default allow secure Registry for this you have to establish connection to docker hu registry
```
$ docker login 
$ docker password
```
2. if run your container ``` Docker run ``` command then first locally searched if local image not found then docker go to docker hub
and pull image on local system.

3. if you work on your orgainsation you dont have network connection then how to pull your image to docker server and share to other team members 
then here the main role play local registry server that gonna help your other team member very easily 
 
``` 
docker container run -d -p 5000:5000 --name my_local_registry registry
```
Go to browser and check here 127.0.0.1:5000/v2/.catlog......pretty good!!

4. Now  time to push your customize image to local registry this is intresting things (if you want to attach your registry storage to s3 cloud then u can attach very easily but here i am not show you )

```
docker image tag image_name:version 127.0.0.1:5000/new_image_name
docker image push 127.0.0.1:5000/new_image_name
```
and then go again web browser and see its load there from local system to local registry we can say centrize registry server 

5. Now if other team member require this then easily download without network 
```
docker image pull 127.0.0.1:5000/new_image_name
```
6. if you want to make your local registry insecure then 
go to
```
$ vi daemon.json
{
"insecure-registries" : ["new_ip:5000"]
}

:wq 
and then 
$ mv daemon.json /etc/docker/
$ systemctl docker restart
```

7. if you want to make or create secure registry (your requirement is specific person can go and download then)

```
$ mkdir certs
$ openssl req -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key -x509 -days 365 -out certs/domain.crt
$ common name :repo.docker.local
$ ls
$ cd /etc/docker/
$ ls
$ mkdir certs.d
$ cd certs.d/
$ mkdir repo.local:5000
$ cd
$ ls
$ cp certs/domain.crt /etc/docker/certs.d/repo.docker.local\:5000/ca.crt

$ systemctl docker restart

$ docker container run -d -p 5000:5000 --name secure_registry -v$(pwd)/certs/:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt
-e REGISTRY_HTTP_TLS_KEY=/certs/domain.key registry

go to 
cd /etc/hosts

host_ip    repo.docker.local

$ docker image tag nginx repo.docker.local:5000/nginx
$ docker image push repo.docker.local:5000/nginx

```
8.Now how to authenticate docker registry
```
mkdir auth

and then push your docker image to registry

$ docker tag webserver:v1 <image_name:version> nameof_user_id/image_name
$ docker push user_id_name/image_name

if you want to pull
$ docker run -it user_id/webserver:v1
```
