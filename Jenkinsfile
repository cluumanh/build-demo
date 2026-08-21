pipeline {
    agent any

    stages {
        stage('Build Spring Boot') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t build-demo:latest .'
            }
        }

        stage('Docker Run') {
            steps {
                sh '''
                    docker stop build-demo-app || true
                    docker rm build-demo-app || true

                    docker run -d \
                      --name build-demo-app \
                      -p 8080:8080 \
                      build-demo:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Spring Boot build and Docker deploy SUCCESS!'
        }

        failure {
            echo 'Pipeline FAILED!'
        }
    }
}