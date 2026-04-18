pipeline {
  agent any

  environment {
    IMAGE_NAME = 'dhar888/cicd-app:latest'
  }

  stages {

    stage('Build Docker Image') {
      steps {
        bat 'docker build -t %IMAGE_NAME% .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub-cred',
          usernameVariable: 'USERNAME',
          passwordVariable: 'PASSWORD'
        )]) {
          bat 'docker login -u %USERNAME% -p %PASSWORD%'
          bat 'docker push %IMAGE_NAME%'
          bat 'docker logout'
        }
      }
    }
    stage('Test K8s') {
      steps {
        bat 'set KUBECONFIG=C:\\Users\\Dharani\\.kube\\config && kubectl get pods'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        bat 'set KUBECONFIG=C:\\Users\\Dharani\\.kube\\config && kubectl apply -f deployment.yaml'
      }
    }
    
    }
  }
}
