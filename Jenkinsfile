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
            sh(script: 'gradle build', label: 'gradle build')
            sh './gradlew javadoc'
            echo 'Archiving artifacts...'
            archiveArtifacts 'build/libs/*.jar'
            junit(testResults: 'build/reports/tests/test', allowEmptyResults: true)
          }
     }
  }
}