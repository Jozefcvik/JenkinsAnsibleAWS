# JenkinsAnsibleAWS

# EC2 Jenkins Server Setup (Ubuntu EC2 t2.micro)

## 📌 Jenkins Server on Ubuntu EC2 (t2.micro)

### 🧰 Step 1: Install Jenkins

#### 1.1 Install Java JDK

- Check available Java versions:
  ```bash
  sudo apt list | grep java

- Install javajdkxx:
  ```bash
  sudo apt install java-jdkxx

#### 1.2 Install JENKINS
  ```bash
  sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
	echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ \
  | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
	sudo apt-get update
	sudo apt-get install jenkins

- Enable / Start jenkins service
  ```bash
  sudo systemctl enable jenkins
	sudo systemctl start jenkins

#### GITHUB PUSH TO JENKINS

GitHub 
 - generate Developer token (classic)

Jenkins
 - add generated token to Manage Jenkins \ Credentials

Github
 - in the repository
 - Settings
 - Webhooks
  - payload url: http://52.59.251.11:8080/github-webhook/
  - content type:application/x-www-form-urlencoded
  - Enable SSL verification
  - Update Webhook
  - PING should be success

Jenkins
 - freestyle job
 - source code management
  - repository URL: https://github.com/Jozefcvik/JenkinsAnsibleAWS.git
  - credentials: none
 - triggers: GitHub hook trigger for GITScm polling
 - Build Steps:
  - Invoke Ansible Playbook:
    - Ansible
    - /ansible/JenkinsAnsibleAWS/playbook01.yml
    - file or host list - /ansible/JenkinsAnsibleAWS/hosts
    - credentials: root

SAVE 

