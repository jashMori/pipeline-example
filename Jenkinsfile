pipeline {
    agent any
    stages {
        stage("compile") {
            steps {
                javac Test.java
            }
        }
        stage("run") {
            steps {
                java Test
            }
        }
    }
}