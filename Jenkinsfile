npipeline {
    agent any

    environment {
        IMAGE_NAME = "nodejs-app"
        CONTAINER_NAME = "nodejs-test"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME $IMAGE_NAME tail -f /dev/null
                '''
            }
        }

        stage('Verify Node') {
            steps {
                sh 'docker exec $CONTAINER_NAME node -v'
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }
    }
}