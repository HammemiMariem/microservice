pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java'
    }

    environment {
        TOMCAT_HOME = "/home/mariem/tomcat"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                cp target/*.war $TOMCAT_HOME/webapps/
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