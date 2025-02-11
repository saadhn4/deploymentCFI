# Deployment Steps for Web Apps / Websites

## 1. Ensure Local Development is Stable
- Verify that your web app or website is working correctly on your local machine.
- HTML -  `git clone git@github.com:suhailroushan13/htmlCalci.git`
- React - `git clone git@github.com:suhailroushan13/reactCalci.git`

## 2. Push Code to GitHub
- Create a GitHub repository.
- Push the code to GitHub without including `node_modules`.

## 3. Update GitHub Repository Details
- Add a proper **description**.
- Add a **URL**.
- Add relevant **keywords**.
- Create a `README.md` file with project details.

## 4. Purchase a Domain (Compare Prices)
- Namecheap
- Hostinger
- GoDaddy
- BigRock

## 5. Purchase a Cloud Service
- AWS
- Google Cloud Platform (GCP)
- Azure
- DigitalOcean

## 6. Set Up Cloud Account
- Create an account and set up payment on your chosen cloud platform.

## 7. Set Up a Virtual Cloud Server (Droplet) on DigitalOcean
1. Log in to **DigitalOcean**.
2. Navigate to **Droplets** → **Create Droplet**.
3. Choose **Region** (e.g., Bangalore).
4. Select **Ubuntu (latest version)** as the OS.
5. Choose **Shared CPU** → **Basic** → **Intel Premium ($16/mo)**.
6. Choose **Authentication Method**: Select **password**, and create a root password.
7. Enable **metrics monitoring and alerting (free)**.
8. Set **Quantity: 1**, and name the **Hostname** (e.g., meraj, omer, sneha).
9. Click **Create Droplet**.
10. Note down the **Public IP Address** (e.g., `157.245.100.213`).

## 8. Access Droplet via Console
1. Navigate to **Droplets** → Select Droplet → Click **More**.
2. Select **Access Console** → **Launch Droplet Console**.
3. Run:
   ```sh
   sudo apt update && sudo apt upgrade
   ```

## 9. Create a New User and Assign Permissions
1. Create a new user:
   ```sh
   sudo adduser suhail
   sudo chown suhail:suhail /home/suhail
   ```
2. Edit sudoers file:
   ```sh
   sudo nano /etc/sudoers
   ```
   Add below admin user:
   ```sh
   suhail ALL=(ALL) ALL
   ```
3. Assign sudo privileges:
   ```sh
   usermod -a -G sudo suhail
   su suhail
   cd
   ```

## 10. Set Up SSH Key for GitHub
1. Generate an SSH key:
   ```sh
   ssh-keygen -t ed25519 -C "your-email@example.com"
   ```
   Press Enter four times.
2. Copy the public key:
   ```sh
   cd .ssh
   cat id_ed25519.pub
   ```
3. Go to **GitHub** → **Settings** → **SSH & GPG Keys** → **New SSH Key**.
4. Paste the key and save.
5. Configure Git:
   ```sh
   git config --global user.name "your-github-username"
   git config --global user.email "your-email@example.com"
   ```
6. Clone the repository:
   ```sh
   git clone <ssh-url>
   ```

## 11. Connect Cloud Server via SSH on WSL/Windows
1. On WSL/Windows:
   ```sh
   cd .ssh
   cat id_ed25519.pub
   ```
2. Copy the public key and add it to **authorized_keys** in your cloud server:
   ```sh
   cd ~/.ssh
   touch authorized_keys
   nano authorized_keys
   ```
   Paste the key, save (`Ctrl + O`, Enter, `Ctrl + X`).
3. Configure SSH in terminal settings:
   - Add a new profile in the terminal.
   - Set command: `ssh username@your-cloud-ip`

## 12. Install Default Packages
```sh
sudo apt install -y git net-tools
sudo timedatectl set-timezone Asia/Kolkata
sudo apt-get install -y nginx
sudo apt install -y snapd
sudo snap install core
sudo apt-get install -y python3-certbot-nginx
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/
sudo apt install -y python3-pip gcc unzip build-essential
sudo apt-get install -y manpages-dev
sudo apt full-upgrade -y
sudo apt-get autoremove -y
```

## 13. Install Node.js
1. Install NVM:
   ```sh
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```
2. Close and reopen terminal.
3. Install Node.js:
   ```sh
   nvm install 22
   node -v
   npm -v
   ```

## 14. Clone Project and Set Up Nginx
1. Clone the project:
   ```sh
   git clone <ssh-url>
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Install **Nodemon** globally:
   ```sh
   npm i -g nodemon
   ```

## 15. Add Domain and Update DNS
1. Open **DigitalOcean** → **Networking** → **Add Domain**.
2. Add your domain and note the **NS records**.
3. Add two A records (`www` and `@`) pointing to your **Cloud IP**.
4. Update your **Domain DNS Settings** with the cloud NS records.
5. Check updates using **dnschecker.org**.

## 16. Configure Nginx
1. Switch to root user:
   ```sh
   sudo su
   ```
2. Remove default config:
   ```sh
   cd /etc/nginx/sites-enabled/
   sudo rm -rf *
   ```
3. Create a new Nginx config:
   ```sh
   cd /etc/nginx/sites-available
   sudo touch domains
   ```
4. Link the config:
   ```sh
   sudo ln -s /etc/nginx/sites-available/domains /etc/nginx/sites-enabled
   ```
5. Generate config using **nginx.suhail.app**, add domain and port.
6. Edit Nginx config:
   ```sh
   sudo nano /etc/nginx/sites-available/domains
   ```
7. Test and restart Nginx:
   ```sh
   sudo nginx -t
   sudo systemctl restart nginx
   ```

## 17. Start Project Server
1. Navigate to project directory:
   ```sh
   cd repoName/server
   ```
2. Install **Nodemon** and **PM2**:
   ```sh
   npm i -g nodemon pm2
   ```
3. Start project:
   ```sh
   npm start
   ```
4. Run using PM2:
   ```sh
   pm2 start app.js --name "AppName"
   ```
5. Manage PM2 processes:
   ```sh
   pm2 restart all
   pm2 delete <id>
   pm2 restart <id>
   pm2 logs <id>
   ```

---
This guide provides a structured and detailed approach to deploying web applications on DigitalOcean. 🚀

