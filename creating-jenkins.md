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