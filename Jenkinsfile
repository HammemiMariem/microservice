pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java'
    }

    environment {
        TOMCAT_HOME = "/home/mariem/tomcat/webapps"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'cd country-service && mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'cd country-service && mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'cd country-service && mvn package'
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