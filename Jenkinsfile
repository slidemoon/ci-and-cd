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
    stage('restart CMS/LMS') {
      steps {
        try {
          sh '''sudo /edx/bin/supervisorctl restart edxapp:
                sleep 10
                if [ $(sudo /edx/bin/supervisorctl status |grep edxapp: |grep RUNNING  |wc -l) -eq 2 ]; then true; else false; fi
             '''
        } catch (err) {
          echo 'CMS/LMS service down!'
        }
      }
    }
  }
  post {
    success {
      echo 'Succeeded!'
    }
    failure {
      echo 'Failed!'
    }
  }
}