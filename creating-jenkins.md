# Creating Jenkins
![Plan](<Screenshot 2025-02-05 105459.png>)

### Step 1- Login
* Login into one of the servers with user and password provided

### Step 2- Click on New Item

### Step 3- Setting up the new project
1. Type in the name and select 'Freestyle project'
   ![Screenshot](<Screenshot 2025-02-05 120814.png>)
2. Filling in the information, put in a brief description
    ![Screenshot](<Screenshot 2025-02-05 120941.png>)
3. Towards the bottom select 'Add build step'
4. Select 'execute shell'
5. input the command
   ![Screenshot](<Screenshot 2025-02-05 121006.png>)

### Step 6- If you want another project to build straight after one being started
1. Go to the configuration section of the first project 
2. Same setting as before 
3. This time towards the bottom select 'Post build action' and select 'Build other projects'
4. Type in the name of the other project and press apply


## How Jenkins works
![Screenshot of how Jenkins works](<Screenshot 2025-02-06 112043.png>)
* You stage first, then commit and then push
* The git push is the thing that triggers the Jenkins
* The agent nodes first test the code, then merge the code and then deploy the code for users to use within a few min
* Difference between Continuous Deployment and Continuous Delivery is deployment automates the release of each completed chnage and delivery automates the testing performed on chnages stored in CI

## Setting up CI/CD pipeline
### Job 1 - Testing the code and setting up the trigger
![alt text](<Screenshot 2025-02-06 171036.png>)
* On GitHub paste the new public key into the repo settings
* Connect the Jenkins to github by pasting private key to Jenkins

![Screenshot of jenkins setup](<Screenshot 2025-02-06 164239.png>)
* Set up the webhook, by ticking the box 'GitHub hook trigger...'
* Set up webhook from GitHub to send to Jenkins by going onto settings and clicking on Webhooks and then add the url by adding the server Id with the port.
![Screenshot](<Screenshot 2025-02-06 164448.png>)
* Toward the bottom cd into the folder and then npm install and npm start 

### Job2 - Merge the Dev to the main 
* Create dev branch by `git checkout -b dev`
* Create the same as we did for job1 
* Get rid of the hook in job 2 as we don't need it 
 ![Screenshot](<Screenshot 2025-02-10 162834.png>)
* To connect to job1 to job 2
![Screenshots](<Screenshot 2025-02-06 164616.png>)
* Make sure to select the SSH agent box as well and select your credentials
![Screenshot](<Screenshot 2025-02-06 170234.png>)
Plug in method: 
1. Go to SCM section 
2. Put name of repo as origin 
3. Next section as main
    ![Screenshot](<Screenshot 2025-02-10 162953.png>)
4. Get rid of the execute shell
5. Go to post build action, add git publisher
6. Select push only if succeed and select merge option
7. Again in the sections put origin first and then main

### Job 3 - Pulls code from job 1, scp from jenkin to ec2 instance, deploys the changes made to the code
* Set up the same as per usual as stated in job 2
* connect Job 3 to job 2 by going into job 2 and adding the project name of job 3

Blocker:
``
#!/bin/bash

#Define Variables
EC2_USER="ubuntu"  # Use "ec2-user" for Amazon Linux
EC2_PUBLIC_IP="34.254.231.47"
APP_DIRECTORY="~/tech501-sparta-app/app"  # Path to your application on EC2
START_COMMAND="pm2 restart app"  # Adjust based on your app (e.g., `systemctl restart myapp`)

#Copy updated code from Jenkins workspace to EC2 using SCP
scp -r -o StrictHostKeyChecking=no * $EC2_USER@$EC2_PUBLIC_IP:$APP_DIRECTORY

#SSH into EC2 and restart the application
ssh -o StrictHostKeyChecking=no $EC2_USER@$EC2_PUBLIC_IP << EOF
    cd $APP_DIRECTORY
    $START_COMMAND  # Restart the application
EOF
``
![Screenshot](<Screenshot 2025-02-07 164930.png>)

New updated code:
![Screenshot](<Screenshot 2025-02-07 175657.png>)
* Have most of it working the issue is now pm2 command which is not being found, minor issue which is causing it to not display on the ec2 instance.

Solution:
![Screenshot](<Screenshot 2025-02-10 152049.png>)
* The complication and reason it wasn't working was due to overcomplicating it with environmental variables. 
* The issue was essentially the path from where it should scp from to the instance wasn't correct

* Change front page of the app = go into the repo of where the app is and into the dev branch, nano into index file
![Screenshot of terminal](<Screenshot 2025-02-10 163202.png>)

Screenshot of it working:
![alt text](<Screenshot 2025-02-10 151333.png>)
![alt text](<Screenshot 2025-02-10 151731.png>)