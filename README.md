# Homelab

### J'ai transformé mon laptop Windows 11 en serveur Docker Desktop.

## Commandes powershell d'installation de Nessus

  mkdir nessus
  
  cd .\nessus\

  docker run -d --name nessus -p 8834:8834 tenableofficial/nessus
  
   ![Installation de Nessus](https://github.com/trolul/Homelab/blob/main/installation%20de%20nessus%20sur%20docker%20desktop.png)

## Nessus scan de mon LAN : 192.168.68.0/22

   ![Installation de Nessus]([https://github.com/trolul/Homelab/blob/main/installation%20de%20nessus%20sur%20docker%20desktop.png](https://github.com/trolul/Homelab/blob/main/nessus-scan.png))

## Commandes powershell d'installation de Nginx Proxy Manager

  docker network create srv-network

  mkdir Nginx
  
  cd .\Nginx\

  docker run -d --name npm-db --network srv-network -e MYSQL_ROOT_PASSWORD=npm -e MYSQL_DATABASE=npm -e MYSQL_USER=npm -e MYSQL_PASSWORD=npm yobasystems/alpine-mariadb:latest

docker run -d --name nginx-proxy-manager --network srv-network -p 8080:8080 -p 81:81 -p 4443:4443 -v ${PWD}\data:/data -v ${PWD}\letsencrypt:/etc/letsencrypt -e DB_MYSQL_HOST=npm-db -e DB_MYSQL_PORT=3306 -e DB_MYSQL_USER=npm -e DB_MYSQL_PASSWORD=npm -e DB_MYSQL_NAME=npm --restart unless-stopped jc21/nginx-proxy-manager:latest

![Installation de Nginx Proxy Manager](https://github.com/trolul/Homelab/blob/main/nginx%20proxy%20manager.png)

## Commandes powershell d'installation de home-assitant

  mkdir home-assitant
  
  cd .\home-assitant\

docker run -d --name homeassistant --network srv-network -p 8123:8123 -v ${PWD}\config:/config -e TZ=America/New_York --restart unless-stopped homeassistant/home-assistant@sha256:8a99004ff832dbd535e6ac4d141042bc31141ff6a86b4d5bb288b3680fbceac1

![Installation de home-assitant](https://github.com/trolul/Homelab/blob/main/home%20assistant.png)

## Commandes powershell d'installation de pi-hole

  mkdir pi-hole
  
  cd .\pi-hole\

  docker run -d --name pihole --network srv-network -p 53:53/tcp -p 53:53/udp -p 80:80 -v ${PWD}\etc-pihole:/etc/pihole -v ${PWD}\etc-dnsmasq.d:/etc/dnsmasq.d -e TZ=America/New_York -e FTLCONF_WEBPASSWORD=Test1234 -e ServerIP=192.168.68.100 --cap-add=NET_ADMIN --restart unless-stopped pihole/pihole:latest

![Installation de pi-hole](https://github.com/trolul/Homelab/blob/main/pi-hole.png)




