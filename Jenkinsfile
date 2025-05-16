pipeline {
    agent any

    stages {
        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'abzhaw', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://172.17.0.2:2375
                            export DOCKER_CLI_EXPERIMENTAL=enabled

                            # Login
                            docker login -u $USERNAME -p $PASSWORD

                            # Ensure a buildx builder exists (ignore if already there)
                            docker buildx create --use multiarch-builder || true

                            # Build for amd64 + arm64 and push the manifest list
                            docker buildx build \
                              --platform linux/amd64,linux/arm64 \
                              -t abzhaw/node-web-app:latest \
                              --push \
                              .
                        '''
                    }
                }
            }
        }
    }
}
