# Deployment Guide for Cloud Server & Nginx Setup

## 1. Connect to Cloud Server

1. **Open Windows Terminal Preview**
2. **Select Cloud Server** from the terminal options.
3. **Check and Note IP Address**
   ```sh
   ifconfig
   ```
   - Look for the network adapter connected to your cloud instance.
   - Note the IP address for later use.


## 2. Nginx Setup (One-Time Configuration)

1. **Switch to Root User**
   ```sh
   sudo su
   ```
2. **Remove Default Nginx Configuration**
   ```sh
   cd /etc/nginx/sites-enabled/
   sudo rm -rf *
   ```
3. **Create a New Nginx Configuration File**
   ```sh
   cd /etc/nginx/sites-available
   sudo rm -rf *
   sudo touch domains
   ```
4. **Link the Configuration File**
   ```sh
   sudo ln -s /etc/nginx/sites-available/domains /etc/nginx/sites-enabled
   ```


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
   

5. **Generate Configuration Using [nginx.suhail.app](https://nginx.suhail.app)**
   - Add your domain and port.
6. **Edit the Nginx Configuration File**
   ```sh
   sudo nano /etc/nginx/sites-available/domains
   ```


7. **Test and Restart Nginx**
   ```sh
   sudo nginx -t
   sudo systemctl restart nginx
   ```


10. **SSL Certificate**
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


