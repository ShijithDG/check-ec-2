pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'https://github.com/ShijithDG/shijith-check-git-jenkins.git'
            }
        }

        stage('Run Script') {
            steps {
                // Run the Python script
                sh 'python3 addition.py > output.txt'
                sh 'sudo apt-get update && sudo apt-get install -y awscli'
            }
        }

        stage('Archive Artifact') {
            steps {
                // Archive the output file one
                archiveArtifacts artifacts: 'output.txt', fingerprint: true
            }
        }
        stage('making artifacts'){
            steps{
                sh 'tar -cvf my_app.tar.gz addition.py mul.py ' 
            }
        }
        stage('deploy-artifact-s3 '){
            steps{
                withCredentials([[
                    $class:'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'jenkins-S3'
                ]]){
                    sh 'aws s3 cp my_app.tar.gz s3://shijith-jenkins --region ap-south-1'
                }
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
