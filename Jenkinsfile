pipeline {
    agent any
    stages {
        stage('CI') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'nexus' , usernameVariable: 'nexus_username', passwordVariable: 'nexus_pass')]) 
                {
                 
               sh """
               docker build  -t nodejsapp:latest .
               docker login  -u ${nexus_username} -p ${nexus_pass} http://192.168.49.2:30082/repository/docker-repo/
               docker tag nodejsapp:latest  http://192.168.49.2:30082/repository/docker-repo/nodejsapp:latest
               docker push  http://192.168.49.2:30082/repository/docker-repo/nodejsapp:latest
               """
                }
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

