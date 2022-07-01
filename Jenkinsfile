pipeline {
    agent any
    stages {
        stage('CI') {
            steps {
               sh """
               docker build  -t nodejsapp:latest .
               """
                }
            }
        

        stage('CD') {
            steps {
               sh """
               docker run -p 3000:3000 -d nodejsapp:latest
               """
            }
        }
    }
}

