Task 1: Jenkins Automation (Freestyle Maven Jobs)
A) Maven Java Project
1. Create Job → maven_java

New Item → Freestyle

SCM → Git → Add repo URL

Branch → main

Build Steps →

mvn clean

mvn install

Post-build →

Archive artifacts → **/*

Build other projects → MavenJava_Test

Save → Build

2. Create Job → MavenJava_Test

SCM → None

Environment → Delete workspace before build

Build Step → Copy artifacts → maven_java → **/*

Post-build → Archive → **/*

Save → Build

B) Maven Web Project
3. Create Job → maven_web_build

SCM → Git (WAR project repo)

Branch → master

Build Steps →

mvn clean

mvn install

Post-build →

Archive → **/*

Build other projects → maven_web_test

Save → Build

4. Create Job → maven_web_test

SCM → None

Environment → Delete workspace

Build Step → Copy artifacts → maven_web_build → **/*

Build Step → mvn test

Post-build →

Archive → **/*

Build other projects → maven_web_deploy (stable only)

Save → Build

5. Create Job → maven_web_deploy

SCM → None

Environment → Delete workspace

Build Step → Copy artifacts → maven_web_test → **/*

Post-build → Deploy WAR

WAR: **/*.war

Context: webapp

Tomcat URL: http://localhost:8080/

Credentials: admin/admin

Save → Build

Pipeline View

Dashboard → +

Create → Build Pipeline View

Upstream Project → maven_web_build

Save

✅ Task 2: Scripted Jenkins Pipeline
1. Create Pipeline Job

New Item → Pipeline

Name: scripted_pipeline

Type: Pipeline

2. Add Script (Jenkinsfile)
node {
    stage('SCM') {
        git url: 'https://github.com/your/repo.git', branch: 'main'
    }
    stage('Build') {
        sh 'mvn clean install'
    }
    stage('Test') {
        sh 'mvn test'
    }
    stage('Archive') {
        archiveArtifacts artifacts: '**/target/*.jar'
    }
}

3. Build Triggers

Poll SCM OR

GitHub hook trigger for GITScm polling

4. Save → Build Now
✅ Task 3: Minikube + Nagios + Docker + AWS Free Tier
Minikube
Start Cluster
minikube start

Create Pod
kubectl run nginx-pod --image=nginx --port=80

Scale Pod
kubectl scale deployment nginx-pod --replicas=3

Expose Service
kubectl expose pod nginx-pod --type=NodePort --port=80

Nagios in Docker
Run Nagios Container
docker run -d --name nagios -p 8080:80 jasonrivers/nagios


Nagios Dashboard → http://localhost:8080/

AWS Free Tier Setup

Go to https://aws.amazon.com

Click Create AWS Account

Enter email → password

Select Free Tier

Add payment (₹2 refundable)

Identity verification

Login to AWS Console

✅ Task 4: Jenkins CI/CD with Webhooks + Email
A) Webhook Trigger
1. Jenkins

Job → Configure

Build Triggers → Check:

GitHub hook trigger for GITScm polling

2. GitHub

Repo → Settings → Webhooks → Add Webhook

Payload URL:

http://<your-ip>:8080/github-webhook/


Content type → application/json

Event → Just the push event

Save

B) Email Notification
Configure SMTP:

Manage Jenkins → Configure System → Email

SMTP Server → smtp.gmail.com

Port → 587

TLS → yes

Credentials → Gmail App Password

Add Post-build Action:
Editable Email Notification

✅ Task 5: Virtual Machine + Web Deployment
1. Create Ubuntu VM

Open VMware/VirtualBox

New VM → Ubuntu ISO

Allocate CPU/RAM

Install Ubuntu

Login

2. Deploy Web App
Install Apache
sudo apt update
sudo apt install apache2 -y

Copy Web Files
sudo cp -r your-app/* /var/www/html/


Restart Apache:

sudo systemctl restart apache2

3. Access Publicly

Find IP:

ifconfig


OR
VM network settings → Bridged Adapter

Open browser:

http://<vm-ip>/