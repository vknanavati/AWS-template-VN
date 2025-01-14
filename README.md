#clone the repository
git clone https://github.com/mindfulcoder49/internship.git

#install docker
sudo snap install docker

#build and run the docker container
sudo docker compose up --build -d

#install certbot
sudo apt install certbot python3-certbot-nginx -y 

#stop the nginx server
sudo systemctl stop nginx.service

#generate the certbot SSL certificates
sudo certbot certonly --standalone -d aisurvivalmag.com -d www.aisurvivalmag.com

#copy your nginx configuration into the nginx conf.d folder
sudo cp nginx.conf /etc/nginx/conf.d/default.conf

#restart the nginx.service
sudo systemctl restart nginx.service
