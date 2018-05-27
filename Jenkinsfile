node {

    stage('Build Environment') {
        echo "Build stage"
        echo "Details of build are: number ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}"
    }

    stage('Test Environment') {
        echo "Test stage"
    }

    stage('Publish Environment') {
        echo "This is the publishing stage!"
    }

    stage('Promotion') {
      timeout(time: 30, unit: 'SECONDS') {
        option1 = input message: 'Deploy to Production?', parameters: [choice(choices: 'yes\nno', description: '', name: 'Stage')]
      }
      echo "You chose ${option1}"
    }

    stage('Second option stage') {
      def userInput = true
      def didTimeout = false
      try {
          timeout(time: 1, unit: 'MINUTES') { // change to a convenient timeout for you
              userInput = input(
              id: 'Proceed1', message: 'Was this successful?', parameters: [
              [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
              ])
          }
      } catch(err) { // timeout reached or input false
          def user = err.getCauses()[0].getUser()
          if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
              didTimeout = true
          } else {
              userInput = false
              echo "Aborted by: [${user}]"
          }
      }


        if (didTimeout) {
            // do something on timeout
            echo "no input was received before timeout"
        } else if (userInput == true) {
            // do something
            echo "this was successful"
        } else {
            // do something else
            echo "this was not successful"
            currentBuild.result = 'FAILURE'
        }

    }


    stage
}
