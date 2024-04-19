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
                    playbook: '01.install-flask.yml',
                    inventory: 'hosts.ini'
                )
            }
        }
    }
    post {
        success {
            script {
                // Send email for successful deploy
                mail to: 'towehcorina@gmail.com, devopsclass0124@gmail.com',
                subject: "Deploy Successful - ${currentBuild.fullDisplayName}",
                body: "The deploy was successful.\n\nCheck console output at ${BUILD_URL}"
            }
        }
        failure {
            script {
                // Send email for failed deploy
                mail to: 'towehcorina@gmail.com, devopsclass0124@gmail.com',
                subject: "Deploy Failed - ${currentBuild.fullDisplayName}",
                body: "The deploy failed.\n\nCheck console output at ${BUILD_URL}"
            }
        }
    }
}
