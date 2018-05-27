pipeline {
  agent any
  environment {
    check1 = 'no'
    check2 = 'no'
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
            env.check1 = input message: 'Do you want to unpublish V1?', parameters: [choice(choices: 'yes\nno', description: '', name: 'Stage Input 1')]
            echo "You chose ${env.check1}"
            if("${env.check1}" == 'yes') {
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
