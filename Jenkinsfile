pipeline {
  agent any

  environment {
    ARM_CLIENT_ID       = credentials('AZURE_CLIENT_ID')
    ARM_CLIENT_SECRET   = credentials('AZURE_CLIENT_SECRET')
    ARM_TENANT_ID       = credentials('AZURE_TENANT_ID')
    ARM_SUBSCRIPTION_ID = credentials('AZURE_SUBSCRIPTION_ID')
  }

  stages {
    stage('Checkout Code') {
      steps {
        git branch: 'main', url: 'https://github.com/protibha171/protibha6536-terraform-jenkins-lab.git'
      }
    }

    stage('Terraform Init') {
      steps {
        bat 'terraform init'
      }
    }

    stage('Terraform Plan') {
      steps {
        bat '''
          terraform plan
        '''
      }
    }

    stage('Manual Approval') {
      steps {
        input message: 'Approve deployment?', ok: 'Deploy'
      }
    }

    stage('Terraform Apply') {
      steps {
        bat '''
          terraform apply -auto-approve
        '''
      }
    }
  }

  post {
    success {
      echo '✅ Infrastructure provisioned successfully!'
    }
    failure {
      echo '❌ Build failed. Check logs.'
    }
  }
}

