node('master'){

  def dockerImage

  // pull code from github
  stage('Checout SCM'){
    git branch: 'alibek', url: 'https://github.com/fuchicorp/acirustech.git'
  }

  // build socker image
  stage('Build'){
    dockerImage = docker.build("acirustech-alibek")
  }

  //test
  stage('Unit test'){
    dockerImage.inside{
      sh 'ls /app/app.py'
    }
  }

  // push the app to private repository
  stage('Push'){
    docker.withRegistry('htttp://nexus.fuchicorp.com:8086','docker-private-credentials'){
      app.push('${BUILD_NUMBER}')
      app.push('latest')
    }
  }
}