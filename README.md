# Alfresco-Community

# Requirement

Hostname : share
OS : Ubuntu 20.04
HDD : 50 GB - OS
HDD1 : 100 GB - Data (alfresco)
CPU : 8 Core
RAM : 16 GB
Environment : Docker

# Step installation and Configuration

root@share:~# df -h

root@share:~# apt install nmap net-tools network-manager tree python

root@share:~# nmcli dev show ens33

root@share:~# ip -o -f inet addr show | awk '/scope global/ {print $2,$4,$6}'

root@share:~# vim /etc/netplan/00-installer-config.yaml

root@share:~# netplan try

root@share:~# netplan apply

root@share:~# cat /etc/hosts

root@share:~# hostnamectl set-hostname share.com.my --static

root@share:~# hostnamectl set-hostname share.com.my --transient

root@share:~# hostnamectl status

root@share:~# hostnamectl status --static

root@share:~# hostnamectl status --transient

root@share:~#  cat /etc/sysctl.conf | tail -3

root@share:~# sysctl -p

root@share:~# vim /etc/default/grub

root@share:~# update-grub

root@share:~# timedatectl set-timezone Asia/Kuala_Lumpur

root@share:~# timedatectl 

root@share:~# apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

root@share:~# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

root@share:~# add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

root@share:~# apt install docker-ce docker-ce-cli containerd.io

root@share:~# curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

root@share:~# chmod +x /usr/local/bin/docker-compose

root@share:~# ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

root@share:~# usermod -a -G docker admins

root@share:~# id admins

root@share:~# apt install nodejs npm

root@share:~# npm install n -g

root@share:~# n stable

root@share:~# hash -r

root@share:~# npm install -g yo

root@share:~# npm install --global generator-alfresco-docker-installer

root@share:~# cd /share/

root@share:/share# mkdir -p data/alf-repo-data

root@share:/share# mkdir -p logs/alfresco

root@share:/share# mkdir -p data/ocr/input

root@share:/share# mkdir -p data/ocr/output

root@share:/share# mkdir -p keystores/alfresco

root@share:/share# mkdir -p data/solr-data

root@share:/share# mkdir -p data/postgres-data

root@share:/share# mkdir -p logs/postgres

root@share:/share# mkdir -p keystores/solr

root@share:/share# mkdir -p logs/share

root@share:~# chown admins:admins -R /share/

admins@share:~$ cd /share/

admins@share:/share$ yo alfresco-docker-installer

             ,****.
        ,.**. `*****  <-_
       ******** ***** ####
      $********::**** ####;
      _.-._`***::*** ######
    ,*******, *::* .;##### @
    **********,' -=#####',@@@
    ***' .,---, ,.-==@@@@@@@@
     * /@@@@@',@ @\ '@@@@@@@
      '@@@@/ @@@ @@@\ ':#'
      !@@@@ @@@@ @@@@@@@@@^
       @@@@ @@@@@ @@@@@@@'
        `"$ '@@@@@. '##'
             '@@@@;'

     DOCKER COMPOSE ALFRESCO

? Which ACS version do you want to use? 6.2

? How may GB RAM are available for Alfresco (16 is minimum required)? 16

? Do you want to use HTTPs for Web Proxy? Yes

? What is the name of your server? share.com.my

? Choose the password for your admin user admin

? What HTTPs port do you want to use (all the services are using the same port)? 443

? Do you want to use FTP (port 2121)? No

? Do you want to use MariaDB instead of PostgreSQL? No

? Are you using different languages (this is the most common scenario)? Yes

? Do you want to create an internal SMTP server? No

? Do you want to create an internal LDAP server? No

? Select the addons to be installed: Google Docs 3.1.0, JavaScript Console 0.7, Order of the Bee Support Tools 1.0.0.0, Share Site Creators 0.0.8, Simple OCR 2.3.1 (for Alfresco 6.x), Alfresco OCR Transformer 1.0.0 (for Alfresco 7+), ESign C
ert 1.8.2

? Are you using a Windows host to run Docker? No

? Do you want to use a start script? No

root@share:~# tree -f -pug /share/

root@share:~# cat /share/.env 

root@share:/share# chown -R 33007 data/solr-data

root@share:/share# chown -R 999 data/postgres-data

root@share:/share# chown -R 999 logs/postgres

root@share:/share# chown -R 33000 data/alf-repo-data

root@share:/share# chown -R 33000 logs/alfresco

root@share:~# docker pull alfresco/alfresco-content-repository-community:6.2.0-ga

root@share:~# docker pull alfresco/alfresco-search-services:2.0.1

root@share:~# docker pull alfresco/alfresco-share:6.2.0

root@share:~# docker pull alfresco/alfresco-content-app:master

root@share:~# docker pull alfresco/alfresco-transform-misc:2.1.0

root@share:~# docker pull alfresco/alfresco-libreoffice:2.1.0

root@share:~# docker pull alfresco/alfresco-imagemagick:2.1.0

root@share:~# docker pull alfresco/alfresco-pdf-renderer:2.1.0

root@share:~# docker pull alfresco/alfresco-tika:2.1.0

root@share:~# docker pull alfresco/alfresco-share:6.2.0

root@share:~# docker pull alfresco/alfresco-activemq:5.15.8

root@share:~# docker pull postgres:11.4

root@share:~# docker pull nginx:stable-alpine

root@share:~# docker pull jbarlow83/ocrmypdf:latest

root@share:~# cd /share/

root@share:/share# docker-compose up --build --force-recreate -d

root@share:~# docker container ls -a

root@share:~# docker container update --restart=always 43ca907470d6

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/43ca907470d61323d8d85feed660ee5b1eef423743315893963c2e60e2c7402c/hostconfig.json 

root@share:~# docker container update --restart=always 7990ee7b6a7a

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/7990ee7b6a7a3c6f237966777c85edaf672b6987a775c4f769d3dd46336e4148/hostconfig.json 

root@share:~# docker container update --restart=always 088a87251cf7

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/088a87251cf7f0bc13249d9a866b6cf56168a9457c110f0a709b30fb9b898707/hostconfig.json

root@share:~# docker container update --restart=always 05e4768d385d

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/05e4768d385dbee7992b26325c6784826ba676ece3a424f4027a94130902d782/hostconfig.json

root@share:~# docker container update --restart=always 06c3519bf5d8

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/06c3519bf5d8d4ac156783875cd26266baede915f81c822f52efca99cb8a4315/hostconfig.json

root@share:~# docker container update --restart=always d74168a52c63

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/d74168a52c63cca51194998d0c8cbe8bfca7b5d65d5b4c717b08bec2427678ba/hostconfig.json

root@share:~# docker container update --restart=always 96709dc67ff3

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/96709dc67ff39fbb5bfee42161f100511461c20a9af2d3d8dbe9d5e817d8fd21/hostconfig.json

root@share:~# docker container update --restart=always 67d6754dad68

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/67d6754dad6884b3d621540023ab2483a2d86cf4acd793d4ec059b7d37b555c2/hostconfig.json

root@share:~# docker container update --restart=always d3f19d8c1b09

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/d3f19d8c1b09efd0bbe0508e785d894f72957d6a00f1ca580ca72aac5d548067/hostconfig.json

root@share:~# docker container update --restart=always d33f17b42b6f

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/d33f17b42b6f080e8b71ffe90ad17bf706ba959a136b41dc0042cdfddd426170/hostconfig.json

root@share:~# docker container update --restart=always d117ba0ba66f

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/d117ba0ba66fb57bfa962cf178051b49752adf1fd4194dc86b0fed6bb01065b2/hostconfig.json

root@share:~# docker container update --restart=always 0ffc22a2388a

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/0ffc22a2388a30b40c7753e0ebb576238784e88a5bdde64204b29c600818bca7/hostconfig.json 

root@share:~# docker container update --restart=always f596111af531

root@share:~# grep '"RestartPolicy":{"Name":"always","MaximumRetryCount":0}' /var/lib/docker/containers/f596111af531b06640c8fe67bea2ef68b16467211347d2acdfe7637cf5b247d2/hostconfig.json 

root@share:/share# docker-compose ps -a

root@share:/share# docker-compose images

root@share:~# docker ps -a

root@share:~# docker image ls -a

Username : admin

Password : admin

https://share.com.my/alfresco/

https://share.com.my/

https://share.com.my/share/page/

# Reference

https://github.com/Alfresco/alfresco-docker-installer
