# Deployment Steps for Web Apps / Websites

## 1. Ensure Local Development is Stable
- Verify that your web app or website is working correctly on your local machine.
- OR Take below Repo's for Testing
- HTML -  `git clone git@github.com:suhailroushan13/htmlCalci.git`
- React - `git clone git@github.com:suhailroushan13/reactCalci.git`

## 2. Push Code to GitHub
- Create a GitHub repository.
- For HTML follow these Steps : https://upload.suhail.app/uploads/i7NuS8M.txt
- For React follow these Steps : https://upload.suhail.app/uploads/eqTsdG8.txt
- Push the code to GitHub without including `node_modules`.

## 3. Update GitHub Repository Details
- Open your GitHub Repo On Right Side Click On Settings Icon
- Add a proper **description**.
- Add a **URL**. same of Repo URL copy from top URL Box
- Add relevant **keywords**.

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
   Add below admin user or any where in the file
   ```sh
   suhail ALL=(ALL) ALL
   ```
   Then save (`Ctrl + O`, Enter, `Ctrl + X`).
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
# Press Enter 4 times.
2. Copy the public key:
   ```sh
   cd .ssh
   ls
   cat id_ed25519.pub
   ```
3. Go to **GitHub** → **Settings** → **SSH & GPG Keys** → **New SSH Key**.
4. Paste the key and add title as today's date and save.
5. Configure Git:
   ```sh
   git config --global user.name "your-github-username"
   git config --global user.email "your-email@example.com"
   ```

## 11. Connect Cloud Server via SSH on WSL/Windows
 (We have to copy windows .ssh public key and paste in cloud .ssh in a file name called authorized_keys )

## Step 1: Check for `.ssh` Folder in Windows
1. Open **Command Prompt (cmd)**.
2. Type the following command to navigate to the SSH directory:
   ```sh
   cd .ssh
   ```
3. If the folder does not exist, create SSH keys:
   ```sh
   ssh-keygen -t ed25519 -C "your-email@example.com"
   ```
   - Press **Enter** 4 times to accept the default settings.

## Step 2: Copy the Public Key
1. Display the public key:
   ```sh
   dir
   type id_ed25519.pub
   ```
2. Copy the key.

## Step 3: Add the Public Key to Your Cloud Server
1. Open your cloud provider’s terminal or connect via another method.
2. Navigate to the `.ssh` directory:
   ```sh
   exit
   cd
   cd .ssh
   ls
   ```
3. Ensure the `authorized_keys` file exists:
   ```sh
   touch authorized_keys
   nano authorized_keys
   ```
4. Paste the copied public key, save (`Ctrl + O`, Enter, `Ctrl + X`).
5. Close the cloud terminal tab.

## Step 4: Configure SSH in Windows Terminal Preview

1. **Open Windows Terminal Preview**.
2. Click on the **top dropdown menu**.
3. Select **Settings**.
4. On Left Scroll down and **Add a new Profile**.
5. **Duplicate Ubuntu Profile** and rename it as `Cloud Server`.
6. Set the Command Line to:
   ```sh
   ssh username@your-cloud-ip
   ```
7. Save the settings.
8. Close the Terminal

## Step 5: Connect to the Cloud Server
1. Open **Windows Terminal Preview**.
2. Click on the **dropdown menu** and select `Cloud Server`.
3. Enter `yes` when prompted.
4. You are now connected to the cloud server.








## 12. Install Default Packages
1.  
```sh
cd
touch script.sh
nano script.sh
```
2. Copy below all commands and paste it in script.sh
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
3. Save (`Ctrl + O`, Enter, `Ctrl + X`).

4. Run the below command 
```sh
   bash script.sh
```
 

## 13. Install Node.js



1. Install NVM:
   ```sh
   cd
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```
# Close and Reopen terminal.
3. Install Node.js:
   ```sh
   nvm install 22
   node -v
   npm -v
   # To Install Nodemon & pm2
   npm i -g nodemon pm2
   ```


## 15. Add Domain and Update DNS

1. Open **DigitalOcean** → **Networking** → **Add Domain**.
2. Add your domain and note the **NS records**.
3. Add two A records (`www` and `@`) pointing to your **Cloud IP**.  
   ![DNS Settings](https://upload.suhail.app/uploads/-9AsXUE.png)
4. Update your **Domain DNS Settings** with the cloud NS records.
5. Check updates using [dnschecker.org](https://dnschecker.org).
