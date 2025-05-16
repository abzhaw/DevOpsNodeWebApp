pipeline {
    agent any

    stages {
        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'abzhaw', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://172.17.0.2:2375
                            docker login -u $USERNAME -p $PASSWORD
                            docker push abzhaw/node-web-app
                        '''
                    }
                }
            }
        }

    }
}