pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Clonage du dépôt GitHub...'
                checkout scm
            }
        }
        
        stage('Build & Test with Docker') {
            steps {
                echo 'Compilation et tests avec Maven dans Docker...'
                sh '''
                    docker run --rm \
                    -v "${WORKSPACE}":/app \
                    -w /app \
                    maven:3.8.6-openjdk-11 \
                    mvn clean test
                '''
            }
        }
        
        stage('Publish Test Results') {
            steps {
                echo 'Publication des résultats de tests...'
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline exécuté avec succès !'
        }
        failure {
            echo '❌ Le pipeline a échoué.'
        }
        always {
            echo '🔚 Nettoyage terminé.'
        }
    }
}