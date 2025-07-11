pipeline {
  agent any

  stages {
    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Build Application') {
      steps {
        echo '🔧 Building the application...'
        sh 'docker build -t myapp:latest .'
      }
    }

    stage('Test') {
      steps {
        echo '🧪 Running tests...'
        // Replace this with actual tests if any
        sh 'echo "All tests passed!"'
      }
    }

    stage('Deploy with Ansible') {
      steps {
        echo '📦 Deploying with Ansible...'
        sh 'ansible-playbook -i ansible/inventory.ini ansible/deploy.yml'
      }
    }

    stage('Apply Kubernetes Deployment') {
      steps {
        echo '🚀 Applying Kubernetes deployment...'
        withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
          sh 'kubectl apply -f k8s/deployment.yaml'
        }
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

