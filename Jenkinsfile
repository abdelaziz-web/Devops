pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone le dépôt Git
                git url: 'https://github.com/abdelaziz-web/Devops.git', branch: 'main'
            }
        }

        stage('Build Frontend') {
            steps {
                dir('angular-17-client') {
                    script {
                        // Installer les dépendances et construire l'application Angular
                        sh 'npm install'
                        sh 'npm run build --prod'
                    }
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir('spring-boot-server') {
                    script {
                        // Utiliser Maven ou Gradle pour le build backend
                        sh './mvnw clean install' // Si Maven Wrapper est utilisé
                    }
                }
            }
        }
    }

    post {
        always {
            // Archive des fichiers ou rapports de build si nécessaire
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }

        success {
            echo 'Build succeeded!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
