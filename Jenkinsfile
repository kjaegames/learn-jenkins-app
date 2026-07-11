pipeline {
    agent {
        docker {
		        // 강의 자료와 버전을 맞춰주세요! 영상과는 다름!
            image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
            
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage'
                sh '''
		            test -f build/index.html
                    npm test
                '''
            }
        }

        stage('E2E') {
    steps {
        sh '''
            npm install serve
            node_modules/.bin/serve -s build & sleep 10
            npx playwright test
        '''
    }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
