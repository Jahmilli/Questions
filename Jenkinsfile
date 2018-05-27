pipeline {
  agent { any }
  environment {
    check1 = false
    check2 = false
  }
  stages {

    stage('Build Environment') {
        echo "Build stage"
        echo "Details of build are: number ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}"
        echo "Environment variables are ${env.check1} and ${env.check2}"
    }


    stage('Test Environment') {
        echo "Test stage"
    }

    stage('Publish V2') {
      echo "Publishing V2"
    }

    stage('Optional 1: Unpublish V1 or V2?') {
      timeout(time: 2, unit: 'MINUTES') {
        check1 = input id: 'Proceed1', message: 'Do you want to unpublish V1?', parameters: [
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you want to unpublish V1']
        ]
      }
      echo "You chose ${check1}"
      if(check1) {
        echo "Will now unpublish V1"
      } else {
        echo "Will now unpublish V2" //Call an unpublish stage here!
      }
    }

  }
}
