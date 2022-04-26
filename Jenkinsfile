pipeline {
  agent any
  stages {
    stage('cli') {
      steps {
        script {
          setBuildStatus("Build fail", "FAILURE");
        }
        
      }
    }
  }
}

void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/Maxim1802/test3"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "test3"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
