node {

    stage('Build Environment') {
        echo "Build stage"
        echo "Details of build are: number ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}"
    }

    stage('Test Environment') {
        echo "Test stage"
    }

    stage('Optional: Publish New SE') {
      timeout(time: 30, unit: 'SECONDS') {
        option1 = input message: 'Do you want to publish V2?', parameters: [choice(choices: 'yes\nno', description: '', name: 'Stage')]
      }
      echo "You chose ${option1}"
      if(option1 == 'yes') {
        echo "Proceeding to second stage"
      } else {
        echo "Will now unpublish V2" //Call an unpublish stage here!
      }
    }

    stage('Optional: Keep New SE') {
      def userInput = true
      def didTimeout = false
      try {
          timeout(time: 1, unit: 'MINUTES') {
              userInput = input(
              id: 'Proceed1', message: 'Was this successful?', parameters: [
              [$class: 'booleanParam', defaultValue: true, description: '', name: 'Please confirm you agree with this']
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


      if(didTimeout) {
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

}
