pipeline {
    agent any

    environment {
        EC2_HOST = 'ec2-user@ec2-52-66-248-28.ap-south-1.compute.amazonaws.com'
        SSH_CREDENTIALS = credentials('ec2-dev')
    }

   stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'javac Test.java'
            }
        }
        stage('Test') {
            steps {
                bat 'java Test'
            }
        }
        stage('Deploy to EC2') {
            steps {
                script {
                    sshagent(credentials: ['ec2-dev']){
                    bat """
                        scp -o StrictHostKeyChecking=no Test.class ${EC2_HOST}:~
                    """
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
