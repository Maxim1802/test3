pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: cli
            image: amazon/aws-cli
            command:
            - cat
            tty: true
        '''
    }
  }
  stages {

    stage('cli') {
      steps {
        container('cli') {
          sh 'aws --help'
        }
      }
    }
  }
}
