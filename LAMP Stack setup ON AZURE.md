Setting Up LAMP Stack on AZURE:

Setting up a LAMP stack (Linux, Apache, MySQL, PHP) on Azure involves several steps,
including creating a virtual machine (VM), installing the necessary software, and configuring the stack.

Here is a step-by-step guide to help you through the process:

STEP 1.Create a Virtual Machine on Azure:

Log in to the Azure Portal:
Go to portal.azure.com and log in with your credentials.

Create a New VM:
Click on "Create a resource" and select "Virtual Machine".

Choose the appropriate settings:

Subscription: Select your subscription.

Resource Group: Create a new resource group or select an existing one.

VM Name: Enter a name for your VM.

Region: Choose a region close to you.

Image: Select Ubuntu Server (preferably the latest LTS version).

Size: Choose a size that meets your requirements.

Authentication:
Select "SSH public key" for SSH login or "Password" if you prefer using a password.
Configure other necessary settings (e.g., inbound ports for SSH).

Networking and Storage:
Configure the networking settings as required.
Under the “Network settings” we will create a new security group and select “allow SSH 80 traffic from” and “Allow HTTP 443 from the internet”.
This will allow our instance to be able to send and receive traffic, thus be able to connect to the internet.
Leave other settings at their default values unless you have specific requirements.

Review and Create:
Review the VM settings and click "Create". Azure will take a few minutes to deploy your VM.

Step 2: Connect to Your VM via CLI

i. ON YOUR COMMAND PROMPT Connect to Instance:
Establish SSH connection to the VM --

cd "path to your key file" for eg- cd C:\Users\NAME\linux key  (remember to put the cd command before the path)
then, click enter and copy and paste your AZURE CONSOLE SSH (its found when you click on your VM name and click on connect, 
under the 'connect to VM' page click on the SSH client and you will find your VM public DNS that
looks like this az ssh vm --resource-group krystal_group --vm-name krystal --subscription b7e6d027-5a13-4ec9-ae33-10e9a7e0ce13
                   
                                OR

ii. TO CONNECT to your VM VIA YOUR AZURE CLI [BASH OR POWERSHELL (UBUNTU)]-  
ON YOUR AZURE CONSOLE click on your VM name and cick on 'connect',
It will validate, configure and then click on connect.

update to the latest version by running the command - 

sudo apt update

STEP 3.Install Components:

Install Apache:

sudo apt install apache2 -y

Start and Enable Apache:

sudo systemctl start apache2
sudo systemctl enable apache2

Adjust Firewall:
Allow HTTP traffic through the firewall:

sudo ufw allow in "Apache"

Install MySQL:

sudo apt install mysql-server -y

Secure MySQL Installation:

sudo mysql_secure_installation

Follow the prompts to configure MySQL security settings.

Install PHP and Extensions:

sudo apt install php libapache2-mod-php php-mysql -y

STEP 4.Start services
Initiate Apache and MySQL services to ensure functionality.

Restart Apache:
sudo systemctl restart apache2

Restart MySQL:
sudo systemctl restart mysqld

STEP 5.Test LAMP Stack:
Create and access a PHP info file to verify stack operatiION

Create a PHP Info Page:
Create a PHP file in the web root directory: -

sudo nano /var/www/html/info.php

Add the following content:

php
Copy code
<?php
phpinfo();
?>

Save and exit the editor.

Access the PHP Info Page:
Open your web browser and navigate to http://<your-vm-public-ip>/info.php.

voila!!

You should see the PHP information page, indicating that PHP is working correctly.
