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
               sh "docker build -t 19841022/flask ."
               }
         }
         stage('Push image') {
               steps {
               sh 'docker push 19841022/flask'
               }
         }
         stage('ansible deploy') {
               steps {
               sh 'ansible -m ping all'
               sh 'ls'
               sh 'pwd'
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
