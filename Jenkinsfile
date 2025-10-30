pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Clonage du dépôt GitHub...'
                checkout scm
            }
        }
        
        stage('List Files') {
            steps {
                echo 'Contenu du workspace:'
                sh 'ls -la'
                sh 'cat pom.xml'
            }
        }
        
        stage('Build & Test') {
            steps {
                echo 'Compilation et tests avec Maven...'
                sh 'docker run --rm -v ${WORKSPACE}:/app -w /app maven:3.8.6-openjdk-11 mvn clean test'
            }
        }
        
        stage('Publish Results') {
            steps {
                echo 'Publication des résultats...'
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
    
    post {
        success {
            echo '✅ SUCCÈS !'
        }
        failure {
            echo '❌ ÉCHEC'
        }
    }
}