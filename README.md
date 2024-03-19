# Swiggy - (Clone)

Swiggy is an Indian online food ordering and delivery platform. Founded in July 2014, Swiggy is based in Bangalore, and operates in 500 Indian cities, as of September 2021.


![Logo](https://upload.wikimedia.org/wikipedia/en/thumb/1/12/Swiggy_logo.svg/1200px-Swiggy_logo.svg.png)


# Step 1: **Launch EC2 (Ubuntu):**

- Provision an EC2 instance on AWS with Ubuntu AMI and `Instance type t2.large & with 30GB storage`
- create IAM Role with `Administrator permissions` and Attach to EC2-Instance
- Connect to the instance using SSH.

# **Step 2: Clone the Code:**

- First Update all the packages using
```
sudo apt update
sudo su
```

- Clone your application's code repository onto the EC2 instance:
    
    ```bash
    git clone https://github.com/vijaygiduthuri/swiggy.git
    ```
    
# **Step 3: Install Jenkins on EC2-Instance using shell script:**
- `vi script1.sh`

```
#!/bin/bash
sudo su
sudo apt update -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
                  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
                  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
                              /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins
```
- `sudo chmod 777 script1.sh`
- `sh script.sh`

# **Step 5: Install Docker:**

```
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker ubuntu
newgrp docker                                                          
sudo chmod 777 /var/run/docker.sock

```
- `docker --version`

# **Step 6: Run Sonarqube Container:**

```
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

- docker ps -a  : To list all the running containers
- connect to Sonarqube using EC2-Instance PublicIP:port9000     EX: 10.0.0.0:9000

# **Step 7: Intall Trivy, AWSCLI, Terraform using shell script:**
- `vi script2.sh`
  
```
# Install Trivy
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y
# Install Terraform
sudo apt install wget -y
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
# Install AWS CLI 
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt-get install unzip -y
unzip awscliv2.zip
sudo ./aws/install
```

- `sudo chmod 777 script2.sh`
- `sh script2.sh`





## Snap Shots 📷

**Landing Page**

![Logo](https://images2.imgbox.com/d6/35/dapHztFi_o.jpg)

**Register / Log In Drawer controlled via Conditional Rendering**

![Logo](https://images2.imgbox.com/d3/7e/IRjy3CQ5_o.jpg)

**Multi Filter Section Drawer**

![Logo](https://images2.imgbox.com/7f/9f/mz0doOdW_o.jpg)

**Food Details Page**

![Logo](https://images2.imgbox.com/72/e5/bawhJbvf_o.jpg)

**Payment Page**

![Logo](https://images2.imgbox.com/28/2c/NrF6G6p7_o.jpg)


