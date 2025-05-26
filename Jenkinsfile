pipeline {
  agent any

  environment {
    PATH = "${env.PATH}:${env.HOME}/.local/bin"
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/ViorelH/python-ci-cd-demo.git'
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'pip install --user -r requirements.txt'
      }
    }

    stage('Run tests') {
      steps {
        sh 'pytest --junitxml=results.xml'
      }
    }

    stage('Publish test results') {
      post {
        always {
          junit 'results.xml'
        }
      }
    }
  }

  post {
    failure {
      echo '❌ Build failed!'
    }
    success {
      echo '✅ Build succeeded!'
    }
  }
}
