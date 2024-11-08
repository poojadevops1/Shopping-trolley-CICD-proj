pipeline {
    agent any
    tools{
        jdk  'jdk11'
        maven  'maven3'
    }
    
  
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: 'git-cred', poll: false, url: 'https://github.com/poojadevops1/Shopping-trolley-CICD-proj.git'
            }
        }
        
        stage('COMPILE') {
            steps {
                sh "mvn clean compile -DskipTests=true"
            }
        }
        
        
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                script{
                    withDockerRegistry(credentialsId: '2fe19d8a-3d12-4b82-ba20-9d22e6bf1672', toolName: 'docker') {
                        
                        sh "docker build -t shopping-trolley -f docker/Dockerfile ."
                        sh "docker tag  shopping-trolley poojadevops1012/shopping-trolley:1.0.1"
                        sh "docker push  poojadevops1012/shopping-trolley:1.0.1"
                    }
                }
            }
        }
        
        
    }
}
