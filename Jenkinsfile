pipeline {
    agent {
        docker {
            image 'maven:3.8.6-openjdk-11'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Clonage du dépôt GitHub...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Compilation du code Java avec Maven...'
                sh 'mvn clean compile'
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Exécution des tests avec Maven...'
                sh 'mvn test'
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
            echo ' Pipeline exécuté avec succès !'
        }
        failure {
            echo ' Le pipeline a échoué.'
        }
        always {
            echo ' Nettoyage terminé.'
        }
    }
}
