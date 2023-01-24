pipeline {
  agent any
  stages {
    stage('Test') {
        steps {
            echo 'Running unit tests...'
            sh './gradlew test'
            junit 'build/test-results/test/TEST-Matrix.xml'
            echo 'Archiving artifacts...'
            archiveArtifact 'home/ludmila/.jenkins/workspace/TP_Jenkins_main/build/test-results/**/*'
        }
    }
  }
}