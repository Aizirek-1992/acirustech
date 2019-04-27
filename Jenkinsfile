pipeline {
  agent {
    dockerfile {
      filename 'Dockerfile'
    }

  }
  stages {
    stage('Pull SCM') {
      steps {
        sh 'ls /app/app.py'
      }
    }
  }
}