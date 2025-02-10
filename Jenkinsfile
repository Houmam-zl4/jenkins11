pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git branch: 'main', url: 'https://github.com/Houmam-zl4/jenkins11.git'
            }
        }

        stage('Installer les dépendances') {
            steps {
                sh 'npm install'
            }
        }

        stage('Tester le projet') {
            steps {
                script {
                    def testResult = sh(script: 'npm test', returnStatus: true)
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
                sh 'npm run deploy'
            }
        }
    }
}
