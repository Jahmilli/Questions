node {

    stage('Build Environment') {
        echo "Build stage"
        echo "Details of build are: number ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}"
    }

    stage('Test Environment') {
        echo "Test stage"
    }

    stage('Optional: Publish New SE') {
      timeout(time: 1, unit: 'MINUTES') {
        option1 = input message: 'Do you want to publish V2?', parameters: [choice(choices: 'yes\nno', description: '', name: 'Stage Input 1')]
      }
      echo "You chose ${option1}"
      if(option1 == 'yes') {
        echo "Proceeding to second stage"
      } else {
        echo "Will now unpublish V2" //Call an unpublish stage here!
      }
    }

    stage('Optional: Keep New SE') {
      def option2 = 'yes'
      def didTimeout = false
      try {
          timeout(time: 1, unit: 'MINUTES') {
            option2 = input message: 'Do you want to delete the old SE?', parameters: [choice(choices: 'yes\nno',
            description: 'yes: Delete old SE\nno: Initiate rollback', name: 'Optional Input 2'
            )]
          }
      } catch(err) { // timeout reached or input false
          def user = err.getCauses()[0].getUser()
          if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
              didTimeout = true
          } else {
              userInput = 'no'
              echo "Aborted by: [${user}]"
          }
      }


      if(didTimeout) {
          // do something on timeout
          echo "no input was received before timeout"
      } else if (option2 == 'yes') {
          // do something
          echo "this was successful"
      } else {
          // do something else
          echo "this was not successful"
          currentBuild.result = 'FAILURE'
      }

    }

}

// id: 'Proceed1', message: 'Do you want to delete old SE', parameters: [
// [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
// ])
