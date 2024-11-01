pipeline {
    agent { label 'trusted-agent' }  // Spécifie un agent de confiance
    tools {
        maven 'Maven'  // Utilise une installation Maven configurée de manière sécurisée dans Jenkins
    }
    environment {
        // Utilisation de credentials pour les informations sensibles
        MY_SECRET = credentials('my-secret-id')  // Remplacez 'my-secret-id' par l'ID du credential stocké dans Jenkins
    }
    stages {
        stage ('Initialize') {
            steps {
                // Affiche uniquement les informations nécessaires
                echo 'Initializing pipeline...'

                // Evitez d'afficher les variables d'environnement pour des raisons de sécurité
                sh '''
                    echo "Pipeline is configured correctly."
                '''
            }
        }
        
        // Autres étapes de votre pipeline (Build, Test, Deploy, etc.)
        stage ('Build') {
            steps {
                // Exécute des commandes Maven de manière sécurisée sans exposer d'informations sensibles
                sh 'mvn clean package'
            }
        }
    }
    post {
        always {
            // Nettoyage des informations sensibles pour éviter leur fuite dans les logs ou l'environnement
            cleanWs()  // Nettoie l'espace de travail après l'exécution
        }
    }
}
