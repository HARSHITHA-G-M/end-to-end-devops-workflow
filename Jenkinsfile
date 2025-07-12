pipeline {
  agent any

  stages {
    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        echo '🔧 Building Docker image...'
        sh 'docker build -t myapp:latest .'
    }
    }

    stage('Export Docker Image as TAR') {
      steps {
        echo '📦 Saving image as TAR...'
        sh 'docker save myapp:latest -o myapp.tar'
      }
    }

    stage('Load into MicroK8s') {
      steps {
        echo '📥 Importing image into MicroK8s (containerd)...'
        sh 'microk8s ctr image import myapp.tar'
      }
    }

    stage('Run Ansible Playbook') {
      steps {
        echo '📦 Running Ansible deployment...'
        sh 'ansible-playbook -i ansible/inventory.ini ansible/deploy.yml'
      }
    }

    stage('Apply Kubernetes YAMLs via MicroK8s') {
      steps {
        echo '🚀 Deploying to MicroK8s...'
        sh 'microk8s kubectl apply -f k8s/deployment.yaml'
        sh 'microk8s kubectl apply -f k8s/service.yaml'
      }
    }
  }

  post {
    success {
      echo '✅ Deployment completed successfully!'
    }
    failure {
      echo '❌ Deployment failed. Please check logs.'
    }
  }
}

