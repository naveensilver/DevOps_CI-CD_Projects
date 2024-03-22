# Project-1 node-todo-cicd

sudo apt install nodejs
sudo apt install npm

npm install

node app.js

------------------


Accelerate Your Web Application Development with a Jenkins Pipeline Triggered by GitHub Webhook Integration.

[Project-Architecture-Image]

## Project Description:

The project aims to automate the building, testing, and deployment process of a web application using Jenkins and GitHub. The Jenkins pipeline will be triggered automatically by GitHub webhook integration when changes are made to the code repository. The pipeline will include stages such as building, testing, and deploying the application.

## Steps:

### Step-1: Go to EC2 console and Create an EC2 Instance

* Name and Tags : node-todo-cicd

* Application and OS Images : Ubuntu

* Instance type : t2.micro 

* keypair : Proceed without keypair (We will generate laters through `ssh-keygen`)

* Network settings : Default VPC and Default Security Groups 

* Storage : 20GB

* Number of instance : 1

Now Connect to EC2 

### Step-2: Install Jenkins on AWS EC2 Ubuntu instance

1. Install Java: Jenkins requires the Java Runtime Environment (JRE)

* To Install OpenJDK 11, Run:

```
sudo apt update -y                     # Update the latest packages 
sudo apt install openjdk-11-jdk -y     # To install Java-11 Version 
sudo java --version                    # Varify Java Version
```

2. Add Jenkins Repository 

* Start by importing the GPG key. The GPG key verifies package integrity but there is no output.

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

* Add the Jenkins software repository to the source list and provide the authentication key:

```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null
```
3. Install Jenkins 

* Update the system Repository 

```
sudo apt update -y
```

* Now, Install Jenkins by Running 
```
sudo apt-get install jenkins -y 
```

* Varify, Jenkins installed or not ?
```
sudo systemctl status jenkins 
```
Run `ctrl+c` to exit 

[Jenkins RunnING Image]

### Step-3: Install Docker on EC2 instance

* Install Docker 

```
sudo apt-get install docker.io -y
```
* Check Docker Version and Status of Docker

```
docker --version
sudo systemctl status docker
```
Run `ctrl+c` to exit 

* Add your $USER to the docker group:

```
sudo usermod -a -G docker $USER

sudo usermod -a -G docker ubuntu
```
This command adds your current user to the docker group, which grants permission to access the Docker socket.

* Add the Jenkins user to the docker group

```
sudo usermod -a -G docker jenkins
```
This command adds the Jenkins user to the docker group, which grants permission to access the Docker socket.

### Step-4: Generate SSH key 

* Generate the SSH keys for integrating your Jenkins project with your git repository. Use `ssh-keygen` command to create public and private key.

```
ssh-keygen
```
Run below commands to see Public and Private keys 
```
ls -al 

ls .ssh/
```
We can see `authorized_keys` , `id_rsa`: Private , `id_rsa.pub`: Public key. 

* For jenkins we used port 8080

To add port 8080 to an instance, you need to allow traffic on port 8080 in the instance’s security group and configure the instance’s firewall to allow traffic on port 8080.

[<Inbound Rules Image>]

### Step-5: Connect Jenkins Dashboard

* Browse `Your_Instance-public-IP:8080` and It will open Jenkins Dashboard. 
```
Ex: 18.206.165.35:8080/
```

[Image JEkins Dashboard]

* We need an Administrator Password to unlock this. Go to terminal and use below command for password.

```
cat /var/lib/jenkins/secrets/initialAdminPassword
```
and you will get a code like this `277bde9fce12hhd45e980235d6a92e74caf`

Copy and Paste above password in Administrator Password and click on `Continue` and `Install Suggested Plugins`

* Create first admin user

```
User Name : naveensilver

password : 123456

Confirm Password : 123456

Full Name : Naveen Thurkapally 

E-mail : naveensilver136@gmail.com
```

[Image]

Click on `SAVE AND CONTINUE` AND `SAVE AND FINISH`

[Image]

* Jenkins is Ready 

* Start Using Jenkins 

### Step-6: Create a Freestyle Project 

1. In jenkins dashboard, Click on ‘New Item’ button on the left sidebar.

[Image]

2. Give your Project a name and select “Freestyle project” as the project type.

[Image]

3. Go to Configure >> In General, Add description








