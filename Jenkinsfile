pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy') {
            agent { 
                label 'ansible-master' 
            }
            steps {
                echo 'Deploy'
                ansiblePlaybook(
                    playbook: 'install-flask.yml',
                    inventory: 'hosts.ini'
                )
            }
        }
    }
    post {
        success {
            echo 'Flask app deployment successful!'
        }
        failure {
            echo 'Flask app deployment failed!' 
            }
        }
    }
