pipeline {
    agent any

    environment {
        NODE_PATH = 'C:\\Program Files\\nodejs' // Assure que Node.js est bien dans le PATH
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
                    bat 'npm install' // Exécute directement dans cmd.exe
                }
            }
        }

        stage('Tester le projet') {
            steps {
                script {
                    def testResult = bat(script: 'npm test', returnStatus: true)
                    if (testResult != 0) {
                        currentBuild.result = 'FAILURE'
                        error("❌ Les tests ont échoué !")
                    }
                }
            }
        }

        stage('Déployer') {
            when {
                branch 'main'
            }
            steps {
                bat 'npm run deploy'
            }
        }
    }
}
