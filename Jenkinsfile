pipeline {
  environment {
    registry = "akumarvmware/devops-certification"
    registryCredential = 'Welcome@123'
  }
  agent any
  stages {
        stage('Building image') {
        steps{
            script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
        }
        }

        stage('Deploy Image') {
        steps{
            script {
            docker.withRegistry( '', 'dockerhub' ) {
                dockerImage.push()
            }
            }
        }
        }

        stage('Remove Image') {
        steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
        }
        }
   }   
}

node {
    stage('Execute Image'){
        def customImage = docker.build("akumarvmware/devops-certification:${env.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo This code would be executing inside the container.'
        }
    }
}