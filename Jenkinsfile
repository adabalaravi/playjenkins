pipeline {

  environment {
    registry = "ravindra502335/myweb"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/justmeandopensource/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
           dockerImage = docker.build "ravindra502335/myweb" + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
         docker login --username  'ravindra502335' --password 'Jaya@143'
         docker tag 'ravindra502335/myweb' registry + ":$BUILD_NUMBER"
         docker push registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
