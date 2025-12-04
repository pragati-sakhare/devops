pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // The 'scm' variable refers to the SCM configuration defined in the Jenkins job
                checkout scm
            }
        }

        stage('Run Python Script') {
            steps {
                script {
                    // Execute the Python script
                    // Replace 'your_script.py' with the actual name of your Python script
                    sh 'python3 hello.py'
                }
            }
        }
    }
}
