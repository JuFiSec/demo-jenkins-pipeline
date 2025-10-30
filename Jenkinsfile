pipeline {
    agent any

    tools {
        maven 'Maven 3.9'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Clonage du dépôt GitHub...'
                checkout scm
            }
        }
        
        stage('compile & test') {
            steps {
                echo 'Compilation et tests avec Maven...'
                sh 'mvn clean compile'
            }
        }
        
        stage('Build & Test') {
            steps {
                echo 'Compilation et tests avec Maven...'
                sh 'mvn test' 
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