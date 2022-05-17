pipeline {
    agent any
    stages {
        stage('CI') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'docker-iamge' , usernameVariable: 'docker_username', passwordVariable: 'docker_pass')]) {
               sh """
               docker build  -t amllotfy/nodejsApp:latest .
               docker login -u ${docker_username} -p ${docker_pass}
    		   docker push amllotfy/nodejsApp:latest
               
               
               """
                }
            }
        }

        stage('CD') {
            steps {
               sh """
               docker run -p 3000:3000 -d amllotfy/nodejsApp:latest
               """
            }
        }
    }
}