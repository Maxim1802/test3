library identifier: 'custom-lib@main', retriever: modernSCM(
  [$class: 'GitSCMSource',
   remote: 'https://github.com/Maxim1802/explorer-jenkins-lib.git',
   credentialsId: 'explorer_github'])
//@Library("custom-lib") _

pipeline {
  agent any
  stages {
    stage('cli') {
      steps {setBuildStatus(gitUrl: "${GIT_URL}", message: "Build in progress", state: "PENDING")}
    }
    stage('wait') {
      steps {
          sleep(time:10,unit:"SECONDS")  
      }
    }
  }
  post {
    success {setBuildStatus(gitUrl: "${GIT_URL}", message: "Build success", state: "SUCCESS")}
    failure {setBuildStatus(gitUrl: "${GIT_URL}", message: "Build failure", state: "FAILURE")}
  }
}


