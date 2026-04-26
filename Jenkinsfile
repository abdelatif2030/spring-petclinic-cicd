pipeline {
    agent any

    environment {
        IMAGE_NAME = "abdelatif2030/spring-petclinic"
        CONTAINER_NAME = "spring-app"
        PORT = "8083"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abdelatif2030/spring-petclinic-cicd.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t $IMAGE_NAME:latest .
                """
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh """
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE_NAME:latest
                    """
                }
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker rm -f $CONTAINER_NAME || true
                docker run -d --name $CONTAINER_NAME -p $PORT:8080 $IMAGE_NAME:latest
                """
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }

        failure {
            echo "❌ Pipeline failed. Check logs."
        }
    }
}
