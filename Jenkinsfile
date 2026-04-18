pipeline {
  agent any

  environment {
    DOCKERHUB = credentials('dockerhub-cred')
  }

  stages {

    stage('Build Docker Image') {
      steps {
        bat 'docker build -t dhar888/cicd-app:latest .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        bat 'docker login -u %DOCKERHUB_USR% -p %DOCKERHUB_PSW%'
        bat 'docker push dhar888/cicd-app:latest'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        bat 'kubectl apply -f deployment.yaml'
      }
    }
  }
}
