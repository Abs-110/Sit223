pipeline {
  agent any

  environment {
    DIRECTORY_PATH         = 'src/'
    TESTING_ENVIRONMENT    = 'staging'
    PRODUCTION_ENVIRONMENT = 'prod-server'
  }

  stages {
    stage('Build') {
      steps {
        echo "Cloning code from ${env.DIRECTORY_PATH}"
        // sh 'mvn clean compile' or 'npm install'
      }
    }

    stage('Test') {
      steps {
        echo "Running unit tests"
        // sh 'mvn test' or 'npm test'
      }
    }

    stage('Code Quality Check') {
      steps {
        echo "Running SonarQube analysis"
        // withSonarQubeEnv('My SonarQube Server') { sh 'sonar-scanner' }
      }
    }

    stage('Deploy to Staging') {
      steps {
        echo "Deploying to ${env.TESTING_ENVIRONMENT}"
        // sh 'kubectl apply -f k8s/staging/'
      }
    }

    stage('Approval') {
      steps {
        input message: 'Approve deployment to production?', ok: 'Yes, proceed'
      }
    }

    stage('Deploy to Production') {
      steps {
        echo "Deploying to production: ${env.PRODUCTION_ENVIRONMENT}"
        // sh 'kubectl apply -f k8s/prod/'
      }
    }
  }

  post {
    always {
      echo 'Cleaning up...'
    }
    success {
      echo 'Pipeline completed successfully!'
    }
    failure {
      echo 'Pipeline failed. Check logs.'
    }
  }
}
