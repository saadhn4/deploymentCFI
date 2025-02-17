## 1. Add Domain and Update DNS

1. Open **DigitalOcean** → **Networking** → **Add Domain**.
2. Add your domain and note the **NS records**.
3. Add two A records (`www` and `@`) pointing to your **Cloud IP**.  
   ![DNS Settings](https://upload.suhail.app/uploads/-9AsXUE.png)
4. Update your **Domain DNS Settings** with the cloud NS records.
5. Check updates using [dnschecker.org](https://dnschecker.org).


## 2. Connect to Cloud Server

1. **Open Windows Terminal Preview**
2. **Select Cloud Server** from the terminal options.
3. **Check and Note IP Address**
   ```sh
   ifconfig
   ```
   - Look for the network adapter connected to your cloud instance.
   - Note the IP address for later use.





## 3. HTML Setup & Project Deployment

1. **Clone the Project Repository**
   ```sh
   exit
   cd
   git clone <ssh-clone-url>
   ```
2. **Navigate to the Project Directory**
   ```sh
   cd repoName
   ```
3. **Navigate to Server Directory**
   ```sh
   cd server
   ```
4. **Install Dependencies**
   ```sh
   npm i
   ```
5. **Start the Project**
   ```sh
   npm start
   ```
6. **Open Browser and Check**
   - Use your cloud IP and port to verify:
     ```
     http://<cloud-ip>:<port>
     ```
   - Example: `http://64.227.167.135:5001`

-  If you are able to access on browser then stop the server 
   
 **Generate Configuration Using [nginx.suhail.app](https://nginx.suhail.app)**
   - Add your domain and port.

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name suhail.com www.suhail.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}


```


5. **Edit the Nginx Configuration File & Paste in it**
   ```sh
   sudo nano /etc/nginx/sites-available/domains
   ```


6. **Test and Restart Nginx**
   ```sh
   sudo nginx -t
   sudo systemctl restart nginx
   ```

## Before Generating SSL Certificates check A Record and NS Record are Updated from dnschecker.org (A and NS Record)

7. **SSL Certificate**
   ```sh
   sudo su
   certbot --nginx
   Enter your email :
   Type : Y
   Type : Y
   Select your domains by typing number 1,2,3
   and make sure you get 
   Successfully 
   Open Broswer and check domain and check ssl certificate 


   ```


8. **Start the Project**
   ```sh
   exit
   cd
   cd repoName
   cd server
   pm2 start app.js --name "Project Name and Port"

   ```

9. **PM2 Commands**
   ```sh
   pm2 list 
   pm2 restart id or name
   pm2 restart all
   pm2 stop id or name 
   pm2 stop all
   pm2 logs 
   pm2 logs id or name

   ```


### Now your server should be accessible via your configured domain or cloud IP. 🚀


#  Second Time Adding Domain or Project 

## 1. Add Domain and Update DNS

1. Open **DigitalOcean** → **Networking** → **Add Domain**.
2. Add your domain and note the **NS records**.
3. Add two A records (`www` and `@`) pointing to your **Cloud IP**.  
   ![DNS Settings](https://upload.suhail.app/uploads/-9AsXUE.png)
4. Update your **Domain DNS Settings** with the cloud NS records.
5. Check updates using [dnschecker.org](https://dnschecker.org).


## 2. HTML Setup & Project Deployment

1. **Clone the Project Repository**
   ```sh
   exit
   cd
   git clone <ssh-clone-url>
   ```
2. **Navigate to the Project Directory**
   ```sh
   cd repoName
   ```
3. **Navigate to Server Directory**
   ```sh
   cd server
   ```
4. **Install Dependencies**
   ```sh
   npm i
   ```
5. **Start the Project**
   ```sh
   npm start
   ```
6. **Open Browser and Check**
   - Use your cloud IP and port to verify:
     ```
     http://<cloud-ip>:<port>
     ```
   - Example: `http://64.227.167.135:5001`

-  If you are able to access on browser then stop the server 
   


5. **Generate Configuration Using [nginx.suhail.app](https://nginx.suhail.app)**
   - Add your domain and port.

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name suhail.com www.suhail.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}


```


6. **Edit the Nginx Configuration File & Paste in it**
   ```sh
   sudo nano /etc/nginx/sites-available/domains
   ```


7. **Test and Restart Nginx**
   ```sh
   sudo nginx -t
   sudo systemctl restart nginx
   ```

## Before Generating SSL Certificates check A Record and NS Record are Updated from dnschecker.org (A and NS Record)

8. **SSL Certificate**
   ```sh
   sudo su
   certbot --nginx
   Enter your email :
   Type : Y
   Type : Y
   Select your domains by typing number 1,2,3
   and make sure you get 
   Successfully 
   Open Broswer and check domain and check ssl certificate 


   ```


9. **Start the Project**
   ```sh
   exit
   cd
   cd repoName
   cd server
   pm2 start app.js --name "Project Name and Port"

   ```

10. **PM2 Commands**
   ```sh
   pm2 list 
   pm2 restart id or name
   pm2 restart all
   pm2 stop id or name 
   pm2 stop all
   pm2 logs 
   pm2 logs id or name

   ```
