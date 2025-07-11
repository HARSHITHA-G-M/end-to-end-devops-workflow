pipeline {
  agent any
  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/your-username/devops-workflow.git'
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
  }
}

