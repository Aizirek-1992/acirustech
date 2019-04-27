node('master') {

  def dockerImage

  // Poll the application to workspace
  stage('Checkout SCM') {
    git 'https://github.com/fuchicorp/acirustech.git'
  }


  // Build the docker image
  stage('Build') {
    dockerImage = docker.build("acirustech-${BRANCH_NAME}")
  }


  // Unitest the application
  stage('Unitest') {
    dockerImage.inside {
      sh 'ls /app/app.py'
    }
  }


  // Push the application to private repository
  stage('Push') {
    docker.withRegistry('http://nexus.fuchicorp.com:8086', 'docker-priv-credentials') {
            dockerImage.push("${BUILD_NUMBER}")
            dockerImage.push("latest")
        }
  }
}