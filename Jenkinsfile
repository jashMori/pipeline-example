pipeline {
    agent any
    environment {
        EC2_HOST = 'ec2-52-66-248-28.ap-south-1.compute.amazonaws.com'
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
                    withCredentials([sshUserPrivateKey(credentialsId: 'ec2-dev', keyFileVariable: 'KEY_FILE')]) {
                        bat """
                            scp -i "%KEY_FILE%" -o StrictHostKeyChecking=no Test.class ec2-user@%EC2_HOST%:~
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
