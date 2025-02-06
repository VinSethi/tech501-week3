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
### Job 1
![alt text](<Screenshot 2025-02-06 171036.png>)
* On GitHub paste the new public key into the repo settings

![Screenshot of jenkins setup](<Screenshot 2025-02-06 164239.png>)
* Connect the Jenkins to github by pasting private key to Jenkins
* Set up the webhook, by ticking the box 'GitHub hook trigger...'
* Set up webhook from GitHub to send to Jenkins by going onto settings and clicking on Webhooks and then add the url by adding the server Id with the port.
![Screenshot](<Screenshot 2025-02-06 164448.png>)
* Toward the bottom cd into the folder and then npm install and npm start 

### Job2
* Create the same as we did for job1 
* To connect to job1 to job 2
![Screenshots](<Screenshot 2025-02-06 164616.png>)
* Make sure to select the SSH agent box as well and select your credentials
![Screenshot](<Screenshot 2025-02-06 170234.png>)