pipeline {
    agent any
    stages {
        stage('CI') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'docker-iamge' , usernameVariable: 'docker_username', passwordVariable: 'docker_pass')]) {
               sh """
               docker build  -t amllotfy/nodejsapp:latest .
               docker login -u ${docker_username} -p ${docker_pass}
    		   docker push amllotfy/nodejsapp:latest
               
               
               """
                }
            }
        }

        stage('CD') {
            steps {
               sh """
               docker run -p 3000:3000 -d amllotfy/nodejsapp:latest
               """
            }
        }
    }
}