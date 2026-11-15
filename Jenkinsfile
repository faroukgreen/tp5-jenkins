
pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Users\\MON PC\\jdk-21.0.12.1'
        PATH = "C:\\Users\\MON PC\\apache-maven-3.10.1-bin\\apache-maven-3.10.1\\bin;${env.PATH}"
        DEPLOY_DIR = 'C:\\deploy-prod'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn -version'
                bat 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'deploy-token', variable: 'TOKEN')]) {
                    bat 'echo Token utilise : %TOKEN%'
                    bat 'if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"'
                    bat 'copy /Y target\\tp5-jenkins-1.0.jar "%DEPLOY_DIR%"'
                }
                echo 'Deploiement termine'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo 'Pipeline reussi'
        }
        failure {
            echo 'Pipeline echoue'
        }
    }
}