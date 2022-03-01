pipeline {
      agent any
      environment{
          DOCKERHUB_CREDENTIALS = credentials('bndah')
      }          
          stages {
               stage('Clone Repository') {
               steps {
               checkout scm
               }
          }
          stage('Build Image') {
               steps {
               sh "docker build -t bndah/mywelcomepage ."
               }
          }
          stage('Login to DockerHub'){
               steps{
                     sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
               } 
          }
         stage('Push image') {
               steps {
               sh 'docker push bndah/mywelcomepage'
               }
         }
         stage('copy the files') {
               steps {
               sh "scp -o StrictHostKeyChecking=no dev.yaml ubuntu@3.83.45.0:/home/ubuntu"
               sh "scp -o StrictHostKeyChecking=no deployans.yml ubuntu@3.83.45.0:/home/ubuntu"
               }
         }       
         stage('ansible deploy') {
               steps {
               sh 'ansible-playbook deployans.yml'
               }
 
         }
         stage('Testing') {
              steps {
                    echo 'Testing...'
                    }
         }
    }
}
                     
