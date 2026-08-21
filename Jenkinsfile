pipeline {
    agent any

    stages {
        stage('Build Spring Boot') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Spring Boot build SUCCESS!'
        }

        failure {
            echo 'Spring Boot build FAILED!'
        }
    }
}