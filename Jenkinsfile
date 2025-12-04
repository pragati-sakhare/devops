pipeline {
    agent {
        docker {
            // Use Ubuntu 22.04 official image
            image 'ubuntu:22.04'
            // Always pull the latest image
            args '-u root:root -v $HOME/.cache/pip:/root/.cache/pip'
        }
    }

    environment {
        PYTHON_CMD = 'python3'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Updating Ubuntu and installing Python...'
                // Install Python 3 and pip inside the container
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-pip git
                '''
            }
        }

        stage('Checkout Code') {
            steps {
                echo 'Checking out code from Git repository...'
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']], // change if your branch is different
                    userRemoteConfigs: [[
                        url: 'https://github.com/pragati-sakhare/devops.git'
                    ]]
                ])
                sh 'ls -l'  // verify files are present
            }
        }

        stage('Install Python Requirements') {
            steps {
                script {
                    if (fileExists('requirements.txt')) {
                        echo 'Installing Python dependencies...'
                        sh "${env.PYTHON_CMD} -m pip install -r requirements.txt"
                    } else {
                        echo 'No requirements.txt found. Skipping.'
                    }
                }
            }
        }

        stage('Run Python Script') {
            steps {
                echo 'Running hello.py...'
                sh "${env.PYTHON_CMD} hello.py"
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
