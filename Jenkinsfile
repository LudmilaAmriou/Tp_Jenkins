pipeline {
  agent any
  stages {
    stage('Test') {
        steps {
            echo 'Running unit tests...'
            sh './gradlew test'
            junit 'build/test-results/test/TEST-Matrix.xml'
            echo 'Archiving artifacts...'
            archiveArtifacts 'build/test-results/**/*'
            echo 'Generation Cucumber report'
            sh './gradlew cucumberReports'
            archiveArtifacts 'build/reports/cucumber/**/*'
           // cucumber buildStatus: 'UNSTABLE',
              //  reportTitle: 'My report',
               // fileIncludePattern: '**/*.json',
               // trendsLimit: 10

        }
    }
  }
}