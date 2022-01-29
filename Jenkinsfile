pipeline {
      agent any
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
               sh 'docker push  bndah/mywelcomepage'
               }
         }
         stage('copy the files') {
               steps {
               sh "scp -o StrictHostKeyChecking=no deploy.yaml ec2-user@54.242.30.185:/home/ubuntu"
               sh "scp -o StrictHostKeyChecking=no ansi.yml ec2-user@54.242.30.185:/home/ubuntu"
               }
         }       
         stage('ansible deploy') {
               steps {
               sh 'ansible -m ping all'
               sh 'ansible-playbook ansi.yml'
               }
         }
         stage('Testing') {
              steps {
                    echo 'Testing...'
                    }
         }
    }
}
