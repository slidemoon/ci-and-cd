pipeline {
  agent {
    node {
      label 'staging-APP'
    }
    
  }
  stages {
    stage('changedir') {
      steps {
        sh '''cd /edx/app/edxapp/edx-platform/
              git log
           '''
      }
    }
  }
}