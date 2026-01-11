pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk21'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                dir('miniProjetDevOps') {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'miniProjetDevOps/target/*.jar', allowEmptyArchive: false
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "Application déployée avec succès sur le serveur de production (simulé)"'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline terminé.'
        }
        success {
            slackSend channel: '#notifications-jenkins', color: 'good', message: "Succès du Pipeline: ${env.JOB_NAME} [Build #${env.BUILD_NUMBER}]"
        }
        failure {
            slackSend channel: '#notifications-jenkins', color: 'danger', message: "Échec du Pipeline: ${env.JOB_NAME} [Build #${env.BUILD_NUMBER}]"
        }
    }
}