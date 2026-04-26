pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/abdelatif2030/spring-petclinic-cicd.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t spring-petclinic:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8083:8080 spring-petclinic:latest || true'
            }
        }
    }
}
