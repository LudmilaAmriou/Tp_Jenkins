pipeline {
  agent any
  stages {
    stage('Test') {
        steps {
            echo 'Running unit tests...'
            sh './gradlew test'
            archiveArtifacts '**/src/test/java/*'
        }
    }
  }
}