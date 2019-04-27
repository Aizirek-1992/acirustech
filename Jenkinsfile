pipeline {
  agent {
    dockerfile {
      filename 'Dockerfile'
    }

  }
  stages {
    stage('Docker Build') {
      agent any
      steps {
        sh 'ls /app/app.py'
      }
    }
    stage('Unittest') {
      steps {
        sh 'pip'
      }
    }
  }
}