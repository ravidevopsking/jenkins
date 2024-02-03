pipeline {
    agent any
    // agent {
    //     node {
    //         label 'AGENT-1' 
    //         // comment in jenkins mention with two slashes(//)
    //         //connecting jenkin server with agent-1 node
    //     }
    // }
    environment { 
        GREETING = 'Hello Jenkins' //environment is set
    }
    options {
        ansiColor('xterm')    // for enabling color
        // timeout(time: 1, unit: 'HOURS')  //if build run more than 1 hour, it will be timedout
        disableConcurrentBuilds()     // at a time multiple builds will not run, i.e one after another only they run 
    }
    parameters {
        //this parameter block is used for dev,prod,qa environments
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Pick something')
    }
    // build
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            when {
                expression { 
                    params.action == 'apply'
                }
            }
            input {
                message "Should we continue?"
                ok "Yes, we should."
                //this block prompts user to continue or abort
                // submitter "alice,bob"
                // parameters {
                //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                // }
            }
            steps {
                sh """
                    echo "this deploy stage is based on 'when' condition"
                    echo "this step is executed and u can see only when u choose 'apply' parameter"
                    echo "if i chose 'destroy' this step will be skipped"
                """
            }
        }
        stage('check params'){
            steps{
                sh """
                    echo "Hello ${params.PERSON}"

                    echo "Biography: ${params.BIOGRAPHY}"

                    echo "Toggle: ${params.TOGGLE}"

                    echo "Choice: ${params.CHOICE}"

                    echo "Password: ${params.PASSWORD}"
                """
            }
        }
    }
    // post build runs after build job runs
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}

