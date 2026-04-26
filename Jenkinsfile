pipeline {
    agent any

    environment {
        IMAGE_NAME = "abdo1997mohamed2030/spring-petclinic"
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
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f k8s/db.yml
                kubectl apply -f k8s/petclinic.yml
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment to Kubernetes successful!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
