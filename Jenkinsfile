pipeline {
  options {
    skipDefaultCheckout true
  }
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }
  }
  stages {
    stage('Clean-up-and-Check-out') {
      steps {
        deleteDir()
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Finalize') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
  environment {
    CI = 'true'
  }
}
