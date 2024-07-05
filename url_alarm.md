## TASK

#### AIM : Need to set up things like if my website goes down with any reason need to send mail for alert

### Step 1: First we have to create one ec2 instance where we are hosting a sample website on which we are going to test our task.


+ Quick step to create an Ec2 instance:

    - Navigate to EC2 Dashboard.
    - Click on "Launch Instance".
    - Choose an AMI.
    - Choose an instance type.
    - Choose or create a key pair.
    - Configure instance details.
    - Configure security group.
    - Review and launch instance.

+ ssh your ec2 intance with your cli

    - Locate your Key Pair File
    - now go to your instace
    - Find the Public DNS (IPv4) of your Instance:
    - Open your Terminal 
    - ssh your instace with this command 
    ```
    ssh -i /path/to/your-key.pem ec2-user@your-public-dns
    ```

+ Go to inside the instance and install the Nginx package.
    ```
    sudo apt-get install nginx
    ```

+ Now used the cd command to change the directory where the html file stored, and edit the index.html with the nano command (Optional)
    ```
    cd /usr/share/nginx/html
    nano index.html
    ```
+ we installed the Nginx web server and host a simple webpage, next we are going to move on to the CloudWatch

### Step 2: Now we set up cloudWatch and canary for track our web page using canary

+ Quick steps to create canary
    - Navigate to CloudWatch
    - Create Canary: Click on "Create canary"
    - Click on "use a blueprint"
    - Select blueprint: "Broken link checker"
    - Configure Canary: Add canary name, runtime, webpage url which website u want to track
    - Configure Permissions: Set up the required IAM roles
    - CLick on "Creat"
+ Now canary track your data in every 5 minitus

### Step 3: Set Up CloudWatch Alarms

+ Navigate to the CloudWatch service
+ Click on "Alarms" in the left-hand menu
+ Click "Create alarm"
+ Choose a metric: 
    - Click on Custom namespaces
    - Select "By canary" and select the metric
+ Define the conditions for the alarm: 
+ Configure actions (Send email with sns)
+ Create the alarm

### Step 4: Configure Email Notifications

+ Navigate to the SNS service.
+ Click on "Create topic".
+ Enter a name and display name for your topic.
+ Click "Create topic" to finish creating your SNS topic.
+ Subscribe your email address

### Step 5: Test and Validate

+ Go inside your ec2 with ssh and stop nginx and verify that you receive email notifications.
