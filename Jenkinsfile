node('master'){
  @Library('CommonLib@master') _
  def common = new com.lib.JenkinsDeployerPipeline()
  def dockerImage
  def branchName = "alibek" //"${scm.branches[0].name}".replaceAll(/^\*\//, '').replace("/", "-").toLowerCase()
  
  @Library('CommonLib@master') _
  def common = new com.lib.JenkinsDeployerPipeline()
  def salckChannel = 'test-message'
  def slackUrl = 'https://fuchicorp.slack.com/services/hooks/jenkins-ci/'
  def slackTokenId = 'slack-token'
  def common.notifyStarted()
  

  @Library('CommonLib@master') _
  def common = new com.lib.JenkinsDeployerPipeline()
  def salckChannel = 'test-message'
  slackUrl = 'https://fuchicorp.slack.com/services/hooks/jenkins-ci/'
  slackTokenId = 'slack-token'


  // pull code from github
  stage('Checout SCM'){
    git branch: 'alibek', url: 'https://github.com/fuchicorp/acirustech.git'
  }

  // build socker image
  stage('Build'){
    dockerImage = docker.build("acirustech-${branchName}")
    
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