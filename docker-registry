#if you upload your customize image to docker registry then
#first you have to make docker.hub id through docker hub website then
#docker by default allow secure registry 
docker login 
docker password


#docker run command run first locally and then image not found then go to docker hub

#how to local registry server that gonna help your other team member
docker container run -d -p 5000:5000 --name my_local_registry registry

#go to browser type 127.0.0.1:5000/v2/.catlog

#now push your image to local registry
#if you want to attach your registry storage to s3 cloud then u can attach that
docker image tag image_name:version 127.0.0.1:5000/new_image_name
docker image push 127.0.0.1:5000/new_image_name

#go again web browser and see
#its load from local server

docker image pull 127.0.0.1:5000/new_image_name

#to make insecure your local registry
vi daemon.json
{
"insecure-registries" : ["new_ip:5000"]
}
save and exit

mv daemon.json /etc/docker/
systemctl docker restart

#how to create secure registry
'''
mkdir certs
openssl req -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key -x509 -days 365 -out certs/domain.crt
common name :repo.docker.local
ls
cd /etc/docker/
ls
mkdir certs.d
cd certs.d/
mkdir repo.local:5000
cd
ls
cp certs/domain.crt /etc/docker/certs.d/repo.docker.local\:5000/ca.crt
'''
service docker restart
docker container run -d -p 5000:5000 --name secure_registry -v$(pwd)/certs/:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt
-e REGISTRY_HTTP_TLS_KEY=/certs/domain.key registry

'''cd /etc/hosts
host_ip    repo.docker.local
docker image tag nginx repo.docker.local:5000/nginx
docker image push repo.docker.local:5000/nginx
'''

#how to authenticate docker registry
mkdir auth





#push your docker image to registry
docker tag webserver:v1 <image_name:version> nameof_user_id/image_name
docker push user_id_name/image_name

#if you want to pull
docker run -it user_id/webserver:v1
