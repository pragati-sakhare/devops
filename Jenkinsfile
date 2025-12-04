pipeline {
    agent {
        kubernetes {
            label 'python-agent'
            defaultContainer 'python'
            yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: python
    image: python:3.11
    command:
    - cat
    tty: true
"""
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code from Git...'
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']], // replace with your branch
                    userRemoteConfigs: [[url: 'https://github.com/pragati-sakhare/devops.git']]
                ])
                sh 'ls -l'  // verify hello.py is present
            }
        }

        stage('Run Python Script') {
            steps {
                echo 'Running hello.py inside Kubernetes pod...'
                sh 'python hello.py'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
