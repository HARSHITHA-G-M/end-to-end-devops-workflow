pipeline {
  agent any
  stages {
    stage('Clone Code') {
      steps {
        git 'https://github.com/HARSHITHA-G-M/end-to-end-devops-workflow.git'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t myapp:latest .'
      }
    }
    stage('Deploy with Ansible') {
      steps {
        sh 'ansible-playbook -i ansible/inventory.ini ansible/deploy.yml'
      }
    }
    stage('Apply Kubernetes') {
      steps {
        sh 'kubectl apply -f k8s/deployment.yaml'
        sh 'kubectl apply -f k8s/service.yaml'
      }
    }
  }
}

