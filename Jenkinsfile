pipeline {
    agent any

    environment {
        EC2_HOST = 'ec2-user@ec2-52-66-248-28.ap-south-1.compute.amazonaws.com'
        SSH_KEY = credentials('MIIEpQIBAAKCAQEA7iYDAq3DVz4PjcQLLLazup1TPfr/Th8VlWEnBg7My3qZWNjwb7quW0ZmvKvyyA0rB8Wn4pwURFr11Mn/W0sWZeH4Fnmnl6e8Ft48ACL8lKfzFyn33u9OR5xQY8sDw/KabmSzNY9YkOhdnCDUvdx5kQR/32YO87CLRbkGI418PkBFkRlov6EBbTZVXvrOCDls3mMSy81CbI66OJk2It7BDgxCQ7DIk76SQUd13iBFTSSnbmXEfzO142VcTuiALku4edCxWZXCWCyxh6fdjcaTUreQ6N1MUN3v29ikQ2dM189VcN1QByLo9SAFBUd6Tgk/GkIy8XfwFBCAp2CI0Xi4FQIDAQABAoIBAFjLq4uwJom9Bieh1VjStqj6SDNwBwml5XJRSy+jDRFBoTPTj7LZNHGsClqG8ntNDaJUPIjuEVB7afXxa1kq4isS2mHm8mpFjIgqTMzwPqVfCfC1IUrqh5GD4yWSaNEDADnxKjDqReeh/GVeiHRSZLGBr/woHaMXTJauqm9PLeg3bpetAQrp8Gi+2xlhzz4e4WBAfNZuJ6rJOgd/4prH02x+IRUB3FpyzPXIFRsAmefP/KR8vHADcs2Djyni+QLiU+GBruQMd7sVc1V9p71c+e1WzuqMtUKX1QDL1fwU2r+LLCdYdjezjVBeFKzvDnYVOC0QIzOLASnOoXYIIyazaPECgYEA9zN7yUoA3TpyUtI4MYpVfB1EAt46s0Qxy+CGo21rbCI6Jg2b9J7cwu6cKDK1wqFD+HI04dGk7VqHvnFQPZjrCckhBWpW9kg8LJQbKghbdhGH8RXvSqWC0IyZDUWkIn6Wyx1dtW7OGnbNcg3wVHYGmfA7bYsGOMFa7YjZmPLcHM8CgYEA9qAKO+9fEcYSH4u+tSIC9Kkhxk/EclEgqZyRW1Lnzjviuup+wCHQQfhPaqLEAsWWdt5sdxlW75STD1SKsb0x2FiK9VWrNWrHLOCZF6S22EENd//l67ffzIozUwWG6vEGIZ7BCzFvXS6f9mBGOXGOFSdB5ZY8Mg4yNX7kio31fdsCgYEAoUbIevG6EJtiHOCj4sZSsU/SoGBmQbC7ID1S+eqYTAskjtEQL485jj/oR12WMe3Oj5fLIo0JIgWPTFNXO2i55z9+OK9BHxrPj3HtKwYazbPwUfyyiqvi5bbk38DQreSS8t8s1QL+mktqDABGDISYF/SggP5Tx9F2RkSjWmMP8gcCgYEAq2hN1JwouiSsweoRULjjzwGh7L/R7BYAmoGr8Qns/ERY78o87/JQWRlosNeRXc/QJKuwPRKKfpcHorcCckfpVdEsOxkglk6xQbqUDH+5aRHFd6qONUclr3Y597C2taFwvnsk9k+Uc/IM0WLWS+RleMRBI31INw3wzYd09et2PNMCgYEA0Q0UPqWdgHvf5AFh6yKNVUa/rn47ttKCqQfunmNXT6UIYQw2IaffG4WCYbE82SOAcSgyQNdzgT7RGpt/42WzjuXFF3WQnqLOmP0Yev2q8aT/uKkPRupRcL6xHru/9IO+3sdxPLSphYj67iaXoW2sA1GhUiXfBuEk6bK0RBCMn6I=')
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
                    bat """
                        scp -i %SSH_KEY% Test.class ${EC2_HOST}:~
                    """
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