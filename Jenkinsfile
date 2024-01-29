pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    bat 'ng build'
                }
            }
        }

        stage('Copy to XAMPP') {
            steps {
                script {
                    def xamppHtdocs = '\\\\172.16.10.240\\jenkins'
                    def distFolder = 'dist'
                    
                    bat "xcopy /s /y ${distFolder} ${xamppHtdocs}\\"
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }

        failure {
            echo 'Build or deployment failed. Check the Jenkins console output for more details.'
        }
    }
}
