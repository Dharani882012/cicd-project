pipeline {
  agent any

  environment {
    DOCKERHUB = credentials('dockerhub-cred')
  }

  stages {

    stage('Clone Code from GitHub') {
      steps {
        git 'https://github.com/Dharani882012/cicd-project.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t dhar888/cicd-app:latest .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        sh 'docker login -u $DOCKERHUB_USR -p $DOCKERHUB_PSW'
        sh 'docker push dhar888/cicd-app:latest'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }
  }
}
