pipeline{
  agent {
    docker {
      image 'node:16.13.1-alpine'
      args '-p 3000:3000'
    }
  }
  environment {
    HOME = '.'
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm cache clear --force'
        sh 'npm install'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh "chmod +x -R ${env.WORKSPACE}"
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
}