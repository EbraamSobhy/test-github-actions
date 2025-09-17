pipeline {
    agent any

    environment {
        NODE_VERSION = "18"
        NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
        NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/EbraamSobhy/test-github-actions.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Next.js') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Export (Static)') {
            steps {
                sh 'npm run export'
            }
        }

        stage('Deploy to Netlify') {
            steps {
                sh '''
                npx netlify deploy \
                  --dir=out \
                  --site=$NETLIFY_SITE_ID \
                  --auth=$NETLIFY_AUTH_TOKEN \
                  --prod
                '''
            }
        }
    }
}
