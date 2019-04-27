node('master'){

  def dockerImage

  // pull code from github
  stage('Checout SCM'){
    git branch: 'alibek', url: 'https://github.com/fuchicorp/acirustech.git'
  }

  // build socker image
  stage('Build'){
    dockerImage = docker.build("acirustech-${BRANCH_NAME}")
  }

  //test
  stage('Unit test'){
    dockerImage.inside{
      sh 'ls /app/app.py'
    }
  }

  // push the app to private repository
  stage('Push'){
    docker.withRegistry('http://nexus.fuchicorp.com:8086','docker-private-credentials'){
      dockerImage.push('${BUILD_NUMBER}')
      dockerImage.push('latest')
    }
  }
}