pipeline {
  agent {
    node {
      label 'staging-APP'
    }
    
  }
  stages {
    stage('pull code') {
      steps {
        sh '''cd /edx/app/edxapp/edx-platform/
              git branch
              sudo git fetch
              sudo git checkout staging
              sudo git pull
              git branch
              sudo chown -R edxapp:edxapp . 
           '''
      }
    }
  }
}