pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git 'https://github.com/votre-repository.git'
            }
        }

        stage('Installer les dépendances') {
            steps {
                sh 'npm install'
            }
        }

        stage('Tester le projet') {
            steps {
                sh 'npm test'
            }
        }

        stage('Déployer') {
            steps {
                sh 'npm run deploy'
            }
        }
    }
}

