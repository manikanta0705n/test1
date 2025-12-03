.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
--------AWS---------
sudo apt update
sudo apt-get install docker.io
sudo apt install git
>>git clone <githuburl>
ls
cd name
sudo su
sudo docker build -t oles-app .
sudo docker run -d -p 9090:8080 oles-app

-------minikube-----
cmd 
>minikube start
kubectl create deployment mynginx --image=nginx
kubectl expose deployment mynginx --type=NodePort --port=80
kubectl port-forward service/mynginx 8090:80
localhost:8090
--------nagios-------
minikube start
docker pull jasonrivers/nagios
docker run -d --name nagios -p 9090:80 jasonrivers/nagios
localhost:9090
nagiosadmin
nagios
servecies->currentload
------scripted pipeline--------
scripted
pipeline {
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages {
        stage('git repo & clean') {
            steps {
                //bat "rmdir  /s /q mavenjava"
                bat "git clone provide your github link"
                bat "mvn clean -f mavenjava"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f mavenjava" #project name#
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f mavenjava"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f mavenjava"
            }
        }
    }
}



pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages{
        stage("git clone and clean"){
            steps{
                bat "git clone https://github.com/am-varun7/23bd1a0508-test.git"
                bat "mvn clean -f 23bd1a0508-test"
            }
        }
        stage("install"){
            steps{
                bat 'mvn install -f 23bd1a0508-test'
            }
        }
        stage("testing"){
            steps{
                bat 'mvn test -f 23bd1a0508-test'
            }
        }
        stage("package"){
            steps{
                bat 'mvn package -f 23bd1a0508-test'
            }
        }
    }
}
