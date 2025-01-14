## Setting up the AWS server
Set up an EC2 instance with Ubuntu
Open http and https traffic to the world
set up an Elastic IP and associate it with the instance

## Setting up the domain name
buy a domain name
point it at your instance by adding an A record to the DNS pointing at your Elastic IP

## Installing your app on the server

Log in to the AWS server, the easiest way is using EC2 Instance Connect in the browser. Then follow the steps below:

### clone the repository
git clone https://github.com/mindfulcoder49/internship.git

### install docker
sudo snap install docker

### build and run the docker container
sudo docker compose up --build -d

### install certbot
sudo apt install certbot python3-certbot-nginx -y 

### stop the nginx server
sudo systemctl stop nginx.service

### generate the certbot SSL certificates - REPLACE DOMAIN.COM WITH YOUR DOMAIN
sudo certbot certonly --standalone -d domain.com -d www.domain.com

### edit the nginx.conf file to put in your domain name
nano nginx.conf

### copy your nginx configuration into the nginx conf.d folder
sudo cp nginx.conf /etc/nginx/conf.d/default.conf

### restart the nginx.service
sudo systemctl restart nginx.service
