pipeline {
    agent any
    stages {
        stage('CI') {
            steps {
               sh """
               docker build  -t nodejsapp:latest .
               docker login http://nexussvcclusterip:80/repository/docker-repo/
               docker tag nodejsapp:latest 
               docker push nexussvcclusterip:80/repository/docker-repo/nodejsapp:latest
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

