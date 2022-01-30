pipeline {
      agent any
      environment{
         registry = "bndah/dev" 
         registryCredential = 'bndah' 
         dockerImage = '' 
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
         stage('Push image') {
               steps {
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                }
         }
         stage('copy the files') {
               steps {
               sh "scp -o StrictHostKeyChecking=no deploy.yaml ec2-user@3.91.219.178:/home/ec2-user"
               sh "scp -o StrictHostKeyChecking=no ansi.yml ec2-user@3.91.219.178:/home/ec2-user"
               }
         }       
         stage('ansible deploy') {
               steps {
               sh 'ansible -m ping all'
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
