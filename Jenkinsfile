pipeline {
      agent any
      environment{
      DOCKERHUB_CREDENTIALS = credentials('DockerHub')
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
         
         stage('Deploy kubernetes'){
              steps{
              sh 'kubectl apply -f deployans.yml'
              }
         }
         stage('Testing') {
              steps {
                    echo 'Testing...'
                    }
         }
}
}
