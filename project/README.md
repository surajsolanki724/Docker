## Pre-configurations needed:
I am using RedHat Enterprise Linux. Plus I have also installed Docker Software in it. You can use any OS and inside that OS you should have docker software installed. There might be a possibility that some Linux command might be different from other OS but I will explain what is the work of that command.

## Setting up the required things:

# Disabling firewall:
Firewall might block some networking stuffs that's why I at first stopped the firewall.
Use systemctl stop firewalld.

# Starting the docker:
Use systemctl start docker to start Docker Service.

# Downloading required images:
Pulling MySQL Image:
Use docker pull mysql:5.6 to download the mysql version 5.6 image to use as a database server.
To know more about MySQL Image go to this page: https://hub.docker.com/_/mysql
Pulling wordpress Image:
Use docker pull wordpress:5.1.1-php7.2-apache to download the wordpress Image in which php and apache server is already preconfigured.
To know more about wordpress Image go to this page: https://hub.docker.com/_/wordpress
