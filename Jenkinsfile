pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code from Git repository...'
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']], // Replace with your branch if not 'main'
                    userRemoteConfigs: [[
                        url: 'https://github.com/pragati-sakhare/devops.git'
                    ]]
                ])
            }
        }

        stage('List Workspace') {
            steps {
                echo 'Listing files in Jenkins workspace:'
                sh 'ls -l'
            }
        }

        stage('Run Python Script') {
            steps {
                echo 'Running hello.py...'
                sh 'python3 hello.py'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}

