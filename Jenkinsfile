pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:14.15.1'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''npm config set registry https://registry.npm.taobao.org
npm install
'''
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
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