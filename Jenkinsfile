pipeline {
  agent any
  stages {
    stage('cli') {
      steps {
          setBuildStatus("Build in progress", "PENDING");  
        
      }
    }
    stage('wait') {
      steps {
          sleep(time:10,unit:"SECONDS")  
      }
    }
  }
  post {
    success {
      setBuildStatus("Build success", "SUCCESS");
    }
    failure {
      setBuildStatus("Build failure", "FAILURE");
    }
  }
}

void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
    reposSource: [$class: "ManuallyEnteredRepositorySource", url: "${GIT_URL}"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "test3"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
