pipeline {
    agent any

    environment {
        GIT_BASH = 'C:\\Program Files\\Git\\bin\\bash.exe'  // Définit le chemin vers Git Bash
    }

    stages {
        stage('Cloner le dépôt') {
            steps {
                git branch: 'main', url: 'https://github.com/Houmam-zl4/jenkins11.git'
            }
        }

        stage('Installer les dépendances') {
            steps {
                script {
                    // Utiliser Git Bash pour exécuter npm install
                    bat "'${env.GIT_BASH}' -c 'npm install'" // Utilisation de bat pour Windows avec Git Bash
                }
            }
        }

        stage('Tester le projet') {
            steps {
                script {
                    def testResult = bat(script: "'${env.GIT_BASH}' -c 'npm test'", returnStatus: true)
                    if (testResult != 0) {
                        currentBuild.result = 'FAILURE'
                        error("Les tests ont échoué !")
                    }
                }
            }
        }

        stage('Déployer') {
            when {
                branch 'main'
            }
            steps {
                bat "'${env.GIT_BASH}' -c 'npm run deploy'" // Utilisation de Git Bash pour le déploiement
            }
        }
    }
}
