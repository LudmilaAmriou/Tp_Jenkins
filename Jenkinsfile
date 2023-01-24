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
            cucumber buildStatus: 'UNSTABLE',
                       reportTitle: 'My report',
                       fileIncludePattern: 'target/report.json',
                       trendsLimit: 10
        }
    }


    stage('Code Analysis') {
        steps {
            echo 'Running gradle sonar'
            withSonarQubeEnv('sonar') {
              sh './gradlew sonar'
            }
        }
    }



    stage("Code Quality") {
        steps {
            timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
            }
        }
    }



     stage('Build') {
          steps {
            echo 'Generation .jar and Documentation...'
            sh './gradlew build'
            sh './gradlew javadoc'
            echo 'Archiving artifacts...'
            archiveArtifacts artifacts: 'build/libs/*.jar'
            archiveArtifacts artifacts: 'build/docs/javadoc/**'
            javadoc javadocDir: 'path/to/javadoc', archiveJavadoc: true
            junit(testResults: 'build/reports/tests/test', allowEmptyResults: true)
          }
     }
  }
}