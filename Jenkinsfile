pipeline {
    agent any  // Runs on any available Jenkins agent

    environment {
        GIT_REPO = 'https://github.com/adityaband460/git_automation.git'
        BRANCH = 'main'
        GIT_USER = 'Adityaband460'
        GIT_EMAIL = 'adityaband460@gmail.com'
        PAT = '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'  // Replace with your GitHub PAT
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                sh 'make'  // Runs the Makefile to compile the C++ project
            }
        }

        stage('Run Tests') {
            steps {
                sh './bin/app'  // Run the compiled C++ binary
            }
        }

        stage('Push Back to GitHub') {
            steps {
                sh '''
                git config --global user.name "${GIT_USER}"
                git config --global user.email "${GIT_EMAIL}"
                git add .
                git commit -m "Automated Build - $(date)" || echo "No changes to commit"
                git push https://${PAT}@github.com/adityaband460/git_automation.git ${BRANCH}
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
