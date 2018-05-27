pipeline {
  agent any
  environment {
    check1 = false
    check2 = false
  }
  stages {
    stage('Build Environment') {
      steps {
        echo "Build stage"
        echo "Details of build are: number ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}"
        echo "Environment variables are ${env.check1} and ${env.check2}"
      }

    }


    stage('Test Environment') {
      steps {
        echo "Test stage"
      }
    }

    stage('Publish V2') {
      steps {
        echo "Publishing V2"
      }
    }

    stage('Optional 1: Unpublish V1 or V2?') {
      steps {
        timeout(time: 2, unit: 'MINUTES') {
          script {
            env.check1 = input id: 'Proceed1', message: 'Do you want to unpublish V1?', parameters: [
            [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you want to unpublish V1']
            ]
            echo "You chose ${env.check1}"
            if(${env.check1}) {
              echo "Will now unpublish V1"
            } else {
              echo "Will now unpublish V2" //Call an unpublish stage here!
            }
          }
        }

      }
    }

  }
}
