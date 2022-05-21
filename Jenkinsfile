pipeline {
    agent {label 'ec2-p'}
    stages {
        stage('CI') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'docker-iamge' , usernameVariable: 'docker_username', passwordVariable: 'docker_pass')]) {
               sh """
               docker build  -t 13689/nodejsapp:latest .
               docker login -u ${docker_username} -p ${docker_pass}
    		   docker push 13689/nodejsapp:latest
               
               
               """
                }
            }
        }

        stage('CD') {
            steps {
               sh """
               docker run -p 3000:3000 -d  --env-file env.list 13689/nodejsapp:latest
               """
            }
        }
    }
}
