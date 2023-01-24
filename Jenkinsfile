pipeline {
  agent any
  stages {
    stage('Test') {
        steps {
            echo 'Running unit tests...'
            sh './gradlew test'
            junit 'build/test-results/test/TEST-Matrix.xml'
            archiveartifacts artifacts:'build/libs/**/*.jar', fingerprint: true
        }
    }
  }
}