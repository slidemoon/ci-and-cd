pipeline {
  agent {
    node {
      label 'staging-APP'
    }    
  }
  triggers {
    upstream(upstreamProjects: 'trigger-staging', threshold: hudson.model.Result.SUCCESS)
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
          sh '''sudo /edx/bin/supervisorctl restart edxapp:
                sleep 10
                if [ $(sudo /edx/bin/supervisorctl status |grep edxapp: |grep RUNNING  |wc -l) -eq 2 ]; then true; else false; fi
             '''
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