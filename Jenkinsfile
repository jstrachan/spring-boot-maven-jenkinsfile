pipeline {
  agent {
    kubernetes {
      label 'customer-portal-app'
      yaml '''
  spec:
  containers:
  - name: jnlp
  - name: jdk
    image: openjdk:11-jdk
    command:
    - cat
    tty: true
      '''
    }
  }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        container ('jdk') {
          sh './mvnw package'
        }
      }
    }
  }

  // Steps that run after the pipeline stages complete
  // post {
  //  failure {
  //      // TODO notify?
  //  }
  // }
}
