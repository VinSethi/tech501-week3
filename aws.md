# Creating a 2 tier architecture with AWS
# Importing Key onto AWS
* Create a new key locally in the .ssh folder
* Click on the import key to AWS
* cat 'specify the name of the key'
* Copy and paste the public key into AWS and it will be done

## Step 1- Create App VM on AWS
![Screenshot](<Screenshot 2025-02-05 121006-1.png>)
1. Create a name of the app vm 
2. Make sure to select Ubuntu 22.04 LTS
3. Select the instance type as t3.micro
4. Key pair to the one you imported onto AWS
5. Scrolling down to select the SSH and HTTP option and editing the name of the security group otherwise it throws an error
6. Press launch instance to create

## Step 2- Installing and setting up the app VM
![Screenshot](<Screenshot 2025-02-05 160829.png>)
1. SSH into the VM after clicking on connect on AWS
2. Once you have SSH into VM then run `sudo apt update` && `sudo apt upgrade -y`
3. `sudo apt install nginx -y`
4. `sudo apt enable nginx` `sudo systemctl start nginx`
5. Install npm and node.js: `sudo DEBIAN_FRONTEND=noninteractive bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -"` `sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs`
6. git clone the repo 
7. Install pm2 
8. Check nginx is working 
9. Create reverse proxy by `sudo nano /etc/nginx/sites-available/default` changing the file `try_files $uri $uri/ =404;` to `proxy_pass http://127.0.0.1:3000;`
10. npm install and npm start into the app directory to get the app page working 
![Screenshot](<Screenshot 2025-02-05 162000.png>)

## Step 3- Create the DB VM
![Screenshot](<Screenshot 2025-02-05 160829.png>)
* Same as the one when you created the app VM, however do not select HTTP this time
* SSH into the DB VM
1. `sudo apt update` && `sudo apt upgrade -y`
2. `sudo apt install gnupg curl -y`
3. `curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor` 
4. `echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list`
5. `sudo apt update`
6. Installing mongoDB `sudo apt-get install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6`
7. Enabling and starting `sudo systemctl enable mongod` `sudo systemctl start mongod`
8. `sudo nano /etc/mongod.conf` Change the bindIP to 0.0.0.0

## Step 4-Adding the IP of the app into the DB so they talk
* Go into the DB VM on AWS 
* Add the ip of the app into the DB VM as well as the port
* ![Screenshot](<Screenshot 2025-02-05 163200.png>)

## Step 5- Installing pm2 and connecting the DB and App to get posts working
* Going back to the app VM
* Install pm2 globally on the VM
* Once installed go into the app folder and connect to the DB using this command `export DB_HOST=mongodb://172.31.57.0:27017/posts`
  ![Screenshot of terminal](<Screenshot 2025-02-05 163827.png>)
* run npm install to make sure the app is connected to the DB
* You can now run pm2 start app.js and it will display the posts page
* ![Screenshot](<Screenshot 2025-02-05 164003.png>)