
## Second Time Adding Domain or Project

## 1. Add Domain and Update DNS

1. Open **DigitalOcean** → **Networking** → **Add Domain**.
2. Add your domain and note the **NS records**.
3. Add  A records for sub domain pointing to your **Cloud IP**.  
   ![DNS Settings](https://upload.suhail.app/uploads/fZdblZU.png)
   **Added Sub Domain**.  
   ![DNS Settings](https://upload.suhail.app/uploads/dwczxeA.png)
4. Update your **Domain DNS Settings** with the cloud NS records.
5. Check updates using [dnschecker.org](https://dnschecker.org).


## 2.React Setup & Project Deployment

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
3. **Navigate to Client Directory**
   ```sh
   cd client
   npm i 
   npm run build
   mv dist ../server
   cd ..
   cd server
   npm i
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
    ![DNS Settings](https://upload.suhail.app/uploads/s5SCNnY.png)

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
