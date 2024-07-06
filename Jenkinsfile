pipeline {
    agent any

    environment {
        EC2_HOST = 'ec2-user@ec2-52-66-248-28.ap-south-1.compute.amazonaws.com'
        SSH_KEY = credentials('-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEA7iYDAq3DVz4PjcQLLLazup1TPfr/Th8VlWEnBg7My3qZWNjw
b7quW0ZmvKvyyA0rB8Wn4pwURFr11Mn/W0sWZeH4Fnmnl6e8Ft48ACL8lKfzFyn3
3u9OR5xQY8sDw/KabmSzNY9YkOhdnCDUvdx5kQR/32YO87CLRbkGI418PkBFkRlo
v6EBbTZVXvrOCDls3mMSy81CbI66OJk2It7BDgxCQ7DIk76SQUd13iBFTSSnbmXE
fzO142VcTuiALku4edCxWZXCWCyxh6fdjcaTUreQ6N1MUN3v29ikQ2dM189VcN1Q
ByLo9SAFBUd6Tgk/GkIy8XfwFBCAp2CI0Xi4FQIDAQABAoIBAFjLq4uwJom9Bieh
1VjStqj6SDNwBwml5XJRSy+jDRFBoTPTj7LZNHGsClqG8ntNDaJUPIjuEVB7afXx
a1kq4isS2mHm8mpFjIgqTMzwPqVfCfC1IUrqh5GD4yWSaNEDADnxKjDqReeh/GVe
iHRSZLGBr/woHaMXTJauqm9PLeg3bpetAQrp8Gi+2xlhzz4e4WBAfNZuJ6rJOgd/
4prH02x+IRUB3FpyzPXIFRsAmefP/KR8vHADcs2Djyni+QLiU+GBruQMd7sVc1V9
p71c+e1WzuqMtUKX1QDL1fwU2r+LLCdYdjezjVBeFKzvDnYVOC0QIzOLASnOoXYI
IyazaPECgYEA9zN7yUoA3TpyUtI4MYpVfB1EAt46s0Qxy+CGo21rbCI6Jg2b9J7c
wu6cKDK1wqFD+HI04dGk7VqHvnFQPZjrCckhBWpW9kg8LJQbKghbdhGH8RXvSqWC
0IyZDUWkIn6Wyx1dtW7OGnbNcg3wVHYGmfA7bYsGOMFa7YjZmPLcHM8CgYEA9qAK
O+9fEcYSH4u+tSIC9Kkhxk/EclEgqZyRW1Lnzjviuup+wCHQQfhPaqLEAsWWdt5s
dxlW75STD1SKsb0x2FiK9VWrNWrHLOCZF6S22EENd//l67ffzIozUwWG6vEGIZ7B
CzFvXS6f9mBGOXGOFSdB5ZY8Mg4yNX7kio31fdsCgYEAoUbIevG6EJtiHOCj4sZS
sU/SoGBmQbC7ID1S+eqYTAskjtEQL485jj/oR12WMe3Oj5fLIo0JIgWPTFNXO2i5
5z9+OK9BHxrPj3HtKwYazbPwUfyyiqvi5bbk38DQreSS8t8s1QL+mktqDABGDISY
F/SggP5Tx9F2RkSjWmMP8gcCgYEAq2hN1JwouiSsweoRULjjzwGh7L/R7BYAmoGr
8Qns/ERY78o87/JQWRlosNeRXc/QJKuwPRKKfpcHorcCckfpVdEsOxkglk6xQbqU
DH+5aRHFd6qONUclr3Y597C2taFwvnsk9k+Uc/IM0WLWS+RleMRBI31INw3wzYd0
9et2PNMCgYEA0Q0UPqWdgHvf5AFh6yKNVUa/rn47ttKCqQfunmNXT6UIYQw2Iaff
G4WCYbE82SOAcSgyQNdzgT7RGpt/42WzjuXFF3WQnqLOmP0Yev2q8aT/uKkPRupR
cL6xHru/9IO+3sdxPLSphYj67iaXoW2sA1GhUiXfBuEk6bK0RBCMn6I=
-----END RSA PRIVATE KEY-----')
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