pipeline{
  agent any
  tools {
    git 'git'

  }
    
  stages {
    stage('prepare') {
      steps {
        sh "git --version"
        git branch: 'master', credentialsId: 'Gitlab', url: ' https://github.com/korkt-kim/jenkins-vue.git'
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