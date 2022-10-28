pipeline {
  agent any
  stages {
    stage('cli') {
      steps {setBuildStatus("Build in progress", "PENDING")}
    }
    stage('wait') {
      steps {
        //emailext body: 'test', subject: 'test', to: 'moriarty18.02@gmail.com'
        //emailext body: 'test', subject: 'test', to: 'mtrogaev@ankocorp.com'
        //mail bcc: '', body: '1', cc: '', from: '', replyTo: '', subject: '1', to: 'mtrogaev@ankocorp.com'
        sh 'echo ${TAG_DATE}'
        sh 'echo ${TAG_TIMESTAMP}'
        sh 'echo ${TAG_UNIXTIME}'
        sh 'echo ${BUILD_ID}'
        //sh 'echo sh(script: "echo `date +%s`", returnStdout: true).trim()'
        sh 'echo "BUILD_DATE=$(date +%F-%T)"'
        sh 'echo "BUILD_DATE=$(date +%F)"'
        sh 'echo $(date +%F)'
        sh 'echo "${GIT_URL}"'
          sleep(time:10,unit:"SECONDS")  
        
        //emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        emailext body: 'test', subject: 'test', to: 'moriarty18.02@gmail.com'
      }
    }
  }
  post {
    success {setBuildStatus("Build success", "SUCCESS")}
    failure {setBuildStatus("Build failure", "FAILURE")}
  }
}

void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "${GIT_URL}"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "Jenkins"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
