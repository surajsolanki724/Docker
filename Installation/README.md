#first we install a host machine like redhat, mac, windows
#make a repo of docker
#hope u install your virtual box and redhat os.

cd /etc/yum.repos.d
vim docker.repo

in this file we write
" 
[dockerrepo]
baseurl=https://download.docker.com/linux/centos/7/x86_64/stable/
gpgcheck=0" exit n save

#then install docker 
yum install docker --nobest[nobest means latest]

#start service 
systemstl start docker

#to check docker services status 
systemctl status docker 

#to check docker version
docker version

#installation done hope do it with no error



