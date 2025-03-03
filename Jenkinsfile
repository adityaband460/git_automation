pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', credentialsId: 'your-credentials-id', url: 'git@github.com:your-repo.git'
            }
        }
        stage('Pull Latest Code') {
            steps {
                sh 'git pull origin main'
            }
        }
        stage('Build Project') {
            steps {
                sh 'make all'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'make test'
            }
        }
        stage('Push Changes') {
            steps {
                sh '''
                    git config --global user.email "your-email@example.com"
                    git config --global user.name "Jenkins Automation"
                    git add .
                    git commit -m "Automated Build"
                    git push origin main
                '''
            }
        }
    }
}
