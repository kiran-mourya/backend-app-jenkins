pipeline {
    agent any

    tools {
        jdk 'Java17'
        maven 'Maven3'
        git 'Git'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kiran-mourya/product-service.git',
                credentialsId: 'bd335eea-88b1-4fce-94b5-53e134dee9cf'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests=false'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
