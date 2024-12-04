pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'https://github.com/ShijithDG/check-ec-2.git'
            }
        }

        stage('Run Script') {
            steps {
                // Run the Python script
                sh 'python3 addition.py > output.txt'
            }
        }

        stage('Archive Artifact') {
            steps {
                // Archive the output file one
                archiveArtifacts artifacts: 'output.txt', fingerprint: true
            }
        }
    }
    post{
        success{
            echo 'success'
        }
        failure{
            echo 'failure'
        }
        always{
            echo 'cleaning'
        }
    }
}
