pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Users\\MON PC\\jdk-21.0.12.1'
        PATH = "C:\\Users\\MON PC\\apache-maven-3.10.1-bin\\apache-maven-3.10.1\\bin;${env.PATH}"
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