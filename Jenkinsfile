pipeline {
    agent any

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
                sh 'docker build -t abdelatif2030/spring-petclinic:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push abdelatif2030/spring-petclinic:latest
                    '''
                }
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f spring-app || true
                docker run -d --name spring-app -p 8083:8080 abdelatif2030/spring-petclinic:latest
                '''
            }
        }
    }
}
