pipeline {
  agent any
  stages {
    stage('build'){
        steps{
          sh 'gradle build'

        }
    }

    stage('test'){
       steps{

         sh 'gradle test'

       }
    }
  }
}