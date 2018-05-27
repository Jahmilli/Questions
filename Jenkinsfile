node {
    def check1 = false
    def check2 = false

    stage('Build Environment') {
        echo "Build stage"
        echo "Details of build are: number ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}"
    }

    stage('Test Environment') {
        echo "Test stage"
    }

    stage('Publish V2') {
      echo "Publishing V2"
    }

    stage('Optional 1: Unpublish V1 or V2?') {
      timeout(time: 2, unit: 'MINUTES') {
        // check1 = input message: 'Do you want to unpublish V1?', parameters: [choice(choices: 'yes\nno', description: '', name: 'Stage Input 1')]
        check1 = input id: 'Proceed1', message: 'Do you want to unpublish V1?', parameters: [
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
        ])
      }
      echo "You chose ${check1}"
      if(check1) {
        echo "Will now unpublish V1"
      } else {
        echo "Will now unpublish V2" //Call an unpublish stage here!
      }
    }

    if(check1) {
      stage('Unpublish V1') {
        echo "Unpublishing V1"
      }
    }

    if(check1) {
      stage('Optional: Keep New SE') {
        def didTimeout = false
        try {
            timeout(time: 2, unit: 'MINUTES') {
            //  check2 = input message: 'Do you want to delete the old SE?', parameters: [choice(choices: 'yes\nno',
              //description: 'yes: Delete old SE\nno: Initiate rollback', name: 'Optional Input 2'
              //)]
            check2 = input id: 'Proceed2', message: 'Do you want to delete old SE', parameters: [
              [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
              ])
            }
        } catch(err) { // timeout reached or input false
            def user = err.getCauses()[0].getUser()
            if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
                didTimeout = true
            } else {
                check2 = false;
                echo "Aborted by: [${user}]"
            }
        }
      }
    }

    if(check1 && check2) {
      stage('Delete V1') {
        echo "Deleting V1 as both checks have passed!"
      }
    }

    if(check1 && !check2) {
      stage('Publish V1') {
        echo "Publishing V1!"
      }
    }

    if(!check1|| !check2) {
      stage('Unpublish V2') {
        echo "Unpublishing V2"
        //Need to unpublish a specified SE, whether it be
      }
    }
}

//if(didTimeout) {
    // do something on timeout
  //  echo "no input was received before timeout"
//} else if (check2 == 'yes') {
    // do something
//    echo "this was successful"
//} else {
    // do something else
//    echo "this was not successful"
//    currentBuild.result = 'FAILURE'
//}
//}
