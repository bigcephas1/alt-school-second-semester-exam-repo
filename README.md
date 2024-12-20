# alt-school-second-semester-exam-repo
repository for exam submissiom
# Steps to setup a Server(ec2 instance on aws), configure firewalls(security group), download a web server and deploy a HTML landing page
 Create an AWS Account

Detailed and Step-by-Step Guide on How to Provision a Server

This guide is written for absolute beginners and explains how to provision a Linux server from scratch using Amazon Web Services (AWS). It covers creating an account, launching a server (EC2 instance), and accessing the server remotely.
1. Create an AWS Account

    Open your web browser and visit the AWS website:
    https://aws.amazon.com/

    Sign Up for a Free AWS Account:
        Click on "Create an AWS Account".
        Follow the prompts to enter your email, create a password, and set up your account.
        Add billing details (AWS Free Tier includes free services, but billing info is required).

    Once your account is created, log in to the AWS Management Console.

2. Launch a Virtual Server (EC2 Instance)

We will use AWS EC2 (Elastic Compute Cloud) to launch a virtual server.
Step 1: Go to the EC2 Dashboard

    In the AWS Management Console, search for "EC2" in the search bar and click on it.

    You will see the EC2 Dashboard.

Step 2: Launch an Instance

    Click on "Launch Instance".

    Choose an Amazon Machine Image (AMI):
        Select Ubuntu Server 20.04 LTS (or the latest version).
        Ubuntu is a Linux-based operating system that is widely used for servers.

    Choose Instance Type:
        Select the t2.micro instance type. This is free-tier eligible.

    Configure the Instance:
        Leave all settings as default for now.
        Scroll to the bottom and click "Next".

    Add Storage:
        The default 8GB storage is fine for now. Click "Next".

    Configure Security Group:
        Security groups control access to the server.
        Select "Create a new security group".
        Add the following rules:
            SSH: Port 22, Source: Anywhere (0.0.0.0/0)
            (Allows SSH access so you can connect to the server)
            HTTP: Port 80, Source: Anywhere (0.0.0.0/0)
            (Allows access to websites you host on the server)

    Create or Select a Key Pair:
        A key pair is used to securely log into the server.
        Choose "Create a new key pair".
            Name the key pair (e.g., my-key).
            Select "PEM" format.
        Click "Download Key Pair" and save it securely on your computer.

    Note: Without this key file, you won't be able to access the server!

    Click "Launch Instance" to start the server.

3. Connect to the Server (SSH)

Once the instance is launched, you need to connect to it from your computer using SSH.
Step 1: Locate the Public IP Address

    Go back to the EC2 Dashboard.
    Click on "Instances".
    Select your instance and note the Public IP Address.

Example:

Public IP: 3.123.45.67

Step 2: Use SSH to Connect

On Linux/macOS:

    Open your terminal.

    Navigate to the location where your key pair file (my-key.pem) is saved.

cd /path/to/keyfile

Modify the permissions of the key file (required for SSH):

chmod 400 my-key.pem

Connect to the server using SSH:

ssh -i my-key.pem ubuntu@<your_server_public_ip>

Replace <your_server_public_ip> with your server's actual IP address.

Example:

    ssh -i my-key.pem ubuntu@3.123.45.67

    If prompted, type yes to confirm the connection.

On Windows:

    Download PuTTY (an SSH client) from:
    https://www.putty.org/

    Use PuTTYgen to convert your my-key.pem file to .ppk format:
        Open PuTTYgen > Load the my-key.pem file > Save the private key as my-key.ppk.

    Open PuTTY:
        In the Host Name field, enter ubuntu@<your_server_public_ip>.
        Under Connection > SSH > Auth, browse to your my-key.ppk file.
        Click Open to connect.

4. Install and Set Up Nginx Web Server

    Update the Server: Run this command to update the package list:

sudo apt update

Install Nginx: Install the Nginx web server:

sudo apt install Nginx -y

Start Nginx:

sudo systemctl start Nginx
sudo systemctl enable Nginx

Test Nginx Installation: Open your web browser and go to:

    http://<your_server_public_ip:80>

    You should see the default Nginx page.

5. Deploy Your HTML Page

    Navigate to Nginx Document Root:

cd /var/www/html

Edit or Create an HTML File:

sudo nano index.html

Add Content: Paste a basic HTML structure:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Ukpabi Peter Uchenna's Landing Page</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>My name is Ukpabi Peter Uchenna</h1>
    </header>

    <section>
        <h3>Project Description</h3>
        <small>
            This is a project that demonstrates how to deploy an application using a web server (Nginx) running on a server. Full documentation on how to set up the server (AWS EC2 instance), configure firewalls (security groups), and the deployment steps are available <a href="https://github.com/bigcephas1/alt-school-second-semester-exam-repo.git" target="_blank">here</a>.
        </small>
    </section>

    <section>
        <h3>About Me (Bio)</h3>
        <p>
            My name is Ukpabi Peter Uchenna, a native of Arochukwu Local Government Area, Abia State, Nigeria. I am a skilled web developer with a strong passion for leveraging technology to solve complex problems and deliver efficient solutions. I have extensive knowledge in both web development and DevOps, and I am always working to improve my skills in these areas.
        </p>
        <p>
            I have experience working on multiple projects using HTML, CSS, JavaScript, and various frameworks. My programming expertise includes asynchronous programming, promises, classes, loops, DOM manipulation, conditional statements, rendering, prototypes, inheritance, and more. I am eager to continue learning and growing in my career, and I am excited to contribute my skills to new challenges.
        </p>
        <p>
            In addition to my front-end development skills, I have a strong foundation in back-end technologies, including Node.js, Express.js, and databases like MongoDB and MySQL. I have experience designing and implementing RESTful APIs and working with various authentication and authorization mechanisms to ensure the security of web applications. My ability to work across the full stack has enabled me to contribute to all stages of development, from initial design to final deployment.
        </p>
        <p>
            My interest in DevOps emerged as I began to appreciate the importance of continuous integration and deployment (CI/CD) in the development process. I have gained valuable experience in setting up and managing CI/CD pipelines using tools like Jenkins, GitHub Actions, and GitLab CI. This experience has taught me the value of automation in reducing errors and increasing efficiency, allowing development teams to focus more on innovation and less on repetitive tasks.
        </p>
        <p>
            In the journey of life, my story is one filled with resilience, determination, and a burning passion for education. Growing up in Oyigbo, Rivers State, I navigated a landscape rife with challenges, yet each obstacle became a stepping stone toward realizing my dreams.
        </p>
    </section>

    <footer>
        <p>&copy; 2024 UC Trademark. All rights reserved.</p>
    </footer>
</body>
</html>


Save and Exit:

    Press CTRL + O to save.
    Press CTRL + X to exit.

Restart Nginx:

sudo systemctl restart Nginx

Access Your Page: Open a browser and go to:

    http://<your_server_public_ip:80>

    You should now see your custom HTML page.

6. Security: Configuring the Firewall

    Allow HTTP and SSH traffic:

sudo ufw allow 'Nginx'
sudo ufw allow OpenSSH
sudo ufw enable

Check firewall status:

    sudo ufw status

following these steps

You have successfully:

    Created an AWS account.
    Launched a Linux server (EC2 instance).
    Installed Nginx and deployed an HTML page.
    Configured basic security settings.
    Congratulations

You can now host websites or applications on this server.


#Servers Public Ip

13.48.29.211

#Public IPv4 DNS

ec2-13-48-29-211.eu-north-1.compute.amazonaws.com




