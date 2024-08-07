#terraform pipeline


pipeline {
    agent any
    environment {
        name='akash'
    }
    parameters{
        string (name:'person', defaultValue: 'akash singh', description: 'how are you dear')
        booleanParam (name:'isMale', defaultValue: true)
        choice(name:'city', choices:['delhi', 'mumbai', 'agra'])
    }
    stages {
        stage('Build a command') {
            steps {
               sh '''
               ls
               pwd
               '''
            }
        }
        
        stage('Build') {
            steps {
                echo 'build'
            }
        }
        
        stage('Deploy on test') {
            steps {
                echo 'Deploy on test'
            }
        }
        
        stage('Envourament variable') {
            steps {
               sh 'echo "${Build_ID}"'
               sh 'echo "${name}"'
               sh 'echo "${person}"'
            }
        }
        
        
        stage('continue?') {
            input{
                message "Should we continue?"
                ok "yes we should"
            }
            steps {
                echo 'Deploy on prod'
            }
        }
         stage('Deploy on prod') {
            steps {
                echo 'Deploy on prod'
            }
        }
        post{
            always { 
            echo 'I will always say Hello again!'
            }
        }
    }
}
