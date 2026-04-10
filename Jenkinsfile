pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java'
    }

    environment {
        TOMCAT_HOME = "C:/apache-tomcat-9.0.0"   //  adaptez selon votre chemin
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
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
                bat 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                copy target\\*.war %TOMCAT_HOME%\\webapps\\
                '''
            }
        }
    }

    post {
        success {
            echo 'Déploiement réussi !'
        }
        failure {
            echo 'Échec du pipeline !'
        }
    }
}