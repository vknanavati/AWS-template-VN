## Setting up the AWS server
1. Set up an EC2 instance with Ubuntu
2. Open http and https traffic to the world
3. set up an Elastic IP and associate it with the instance

## Setting up the domain name
1. buy a domain name
2. point it at your instance by adding an A record to the DNS pointing at your Elastic IP

## Installing your app on the server

Log in to the AWS server, the easiest way is using EC2 Instance Connect in the browser. Then follow the steps below:

### clone the repository
First we need to get the code onto the server  
`git clone https://github.com/mindfulcoder49/internship.git`

### install docker
Then we need to install docker  
`sudo snap install docker`

### build and run the docker container
Then we need to build and run the docker container which will set up our app to run on
port 8000  
`sudo docker compose up --build -d`

### install certbot
Then we need to install certbot which will let us generate SSL certificates  
`sudo apt install certbot python3-certbot-nginx -y`

### stop the nginx server
We need to stop the nginx server that's running by default, otherwise it will block the 
letsencrypt certificate generation  
`sudo systemctl stop nginx.service`

### generate the certbot SSL certificates - REPLACE DOMAIN.COM WITH YOUR DOMAIN
We then generate the certificates. Your domain must be set up correctly to point at the server, and you must replace domain.com in the command with your domain name.  
`sudo certbot certonly --standalone -d domain.com -d www.domain.com`

### edit the nginx.conf file to put in your domain name
You also need to edit the nginx.conf file to use your domain name as well  
`nano nginx.conf`

### copy your nginx configuration into the nginx conf.d folder
Then you need to copy that nginx.conf file to the right place so the nginx service can use it  
`sudo cp nginx.conf /etc/nginx/conf.d/default.conf`

### restart the nginx.service
Restart your nginx service and you should be able to see your app when you visit your domain name  
`sudo systemctl restart nginx.service`
