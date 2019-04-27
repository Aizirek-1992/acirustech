node('master') {
  git branch: 'florinen', url: 'https://github.com/fuchicorp/acirustech.git'
}
//Build Docker image
stage('Build'){
  app = docker.build('acirustech-florinen')
}
  //Unitest the aplication
 stage('Unitest'){
   dockerImage.inside {
     sh 'ls /app/app.py'
   }
}
 //Push the image to nexus
 stage('Push') {
   docker.withRegistry('http://nexus.fuchicorp.com:8086' , 'docker-priv-credentials') {
     dockerImage.push("${BUILD_NUMBER}")
     dockerImage.push('latest')
   }
 }