# TravelMemory Application

step1: I created ec2 instance 
step2: SSH into your EC2 instance
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '3.111.198.64' (ED25519) to the list of known hosts.
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
Last login: Sun Aug 10 09:49:20 2025 from 13.233.177.5
[ec2-user@ip-172-31-41-191 ~]$ 
step3:Installed Node.js,npm,git
sudo yum update -y
sudo yum install -y nodejs npm git
step4:Clone the reposiory
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
cd TravelMemory/backend

[ec2-user@ip-172-31-41-191 ~]$ git clone https://github.com/UnpredictablePrashant/TravelMemory.git
Cloning into 'TravelMemory'...
remote: Enumerating objects: 119, done.
remote: Counting objects: 100% (69/69), done.
remote: Compressing objects: 100% (40/40), done.
remote: Total 119 (delta 33), reused 29 (delta 29), pack-reused 50 (from 1)
Receiving objects: 100% (119/119), 198.68 KiB | 1.49 MiB/s, done.
Resolving deltas: 100% (40/40), done.
[ec2-user@ip-172-31-41-191 ~]$ cd TravelMemory/backend
[ec2-user@ip-172-31-41-191 backend]$ 
step5:Install dependencies:
npm install
step6 :create and update .env
installed the mongod
[ec2-user@ip-172-31-41-191 backend]$ sudo systemctl start  mongod
[ec2-user@ip-172-31-41-191 backend]$ sudo systemctl status mongod
● mongod.service - MongoDB Database Server
     Loaded: loaded (/usr/lib/systemd/system/mongod.service; enabled; preset: disabled)
     Active: active (running) since Sun 2025-08-10 10:17:30 UTC; 14s ago
       Docs: https://docs.mongodb.org/manual
   Main PID: 28900 (mongod)
     Memory: 153.9M
        CPU: 872ms
     CGroup: /system.slice/mongod.service
             └─28900 /usr/bin/mongod -f /etc/mongod.conf

Aug 10 10:17:30 ip-172-31-41-191.ap-south-1.compute.internal systemd[1]: Started mongod.service - MongoDB Database Server.
Aug 10 10:17:30 ip-172-31-41-191.ap-south-1.compute.internal mongod[28900]: {"t":{"$date":"2025-08-10T10:17:30.998Z"},"s":"I",  "c":"CONTROL",  "id":7484500, "ctx":"main","msg":"Environment varia>
lines 1-12/12 (END)
[ec2-user@ip-172-31-41-191 backend]$ mongosh
Current Mongosh Log ID: 68987268e643bada8289b03c
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.5.6
Using MongoDB:          7.0.22
Using Mongosh:          2.5.6

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/
In .env i set the mongodb url
PORT=3000
DB_URL=mongodb://127.0.0.1:27017/travelmemory
step 7:backend to test:

[ec2-user@ip-172-31-41-191 backend]$ node index.js
Server started at http://localhost:3000

step8:Install & configure Nginx as a reverse proxy

sudo apt install nginx
sudo nano /etc/nginx/sites-available/default
server {
    listen 80;
    server_name your_domain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

[ec2-user@ip-172-31-41-191 backend]$ sudo nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
sudo systemctl restart nginx

step 9. Frontend & Backend Connection
[ec2-user@ip-172-31-41-191 backend]$ cd ../frontend/src
[ec2-user@ip-172-31-41-191 src]$ ls
App.css  App.js  App.test.js  components  index.css  index.js  logo.svg  reportWebVitals.js  setupTests.js  url.js
 step10:build the front end:
 
npm install
ec2-user@ip-172-31-41-191 src]$ npm run build

> frontend@0.1.0 build
> react-scripts build
[ec2-user@ip-172-31-41-191 backend]$ curl http://127.0.0.1:3000
Travel Memory Application Running[ec2-user@ip-172-31-41-191 backend]$ now ec2 front end application is running.






