pipeline {
    // Utiliser une image Docker spécifique (contient Maven et JDK)
    agent {
        docker {
            image 'maven:3.9-jdk17'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Code cloné depuis GitHub."
                // Le pipeline gère le clonage du code automatiquement
            }
        }
        
        stage('Build & Test') {
            steps {
                echo 'Démarrage de la compilation et des tests...'
                // La commande est exécutée à la racine du workspace, à l'intérieur du conteneur Maven.
                sh 'mvn clean package'
            }
        }
    
        stage('Report') {
            steps {
                echo 'Publication des résultats JUnit.'
                // Publie les résultats des tests
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
    
    post {
        always {
            echo 'Fin du pipeline. Vérification du statut...'
        }
        success {
            echo 'Pipeline terminé avec SUCCÈS.'
        }
        failure {
            echo 'Pipeline terminé en ÉCHEC. Voir les résultats de tests.'
        }
    }
}