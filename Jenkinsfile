pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/adityaband460/git_automation.git'
        BRANCH = 'main'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                sh 'make'
            }
        }

        stage('Run Tests') {
            steps {
                sh './bin/app'
            }
        }

        stage('Push Back to GitHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-credentials', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                    sh '''
                        git config --global user.name "adityaband460"
                        git config --global user.email "adityaband460@gmail.com"
                        git add .
                        date
                        git commit -m "Automated Build - $(date)"
                        git push https://$GIT_USER:$GIT_PASS@github.com/adityaband460/git_automation.git main
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build and Push Successful!"
        }
        failure {
            echo "❌ Build Failed!"
        }
    }
}
