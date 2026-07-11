pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
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
        sh '''
            echo "=== Project Files ==="
            ls -la

            echo "=== Node Version ==="
            node --version
            npm --version

            echo "=== Install Dependencies ==="
            npm ci

            echo "=== Run Tests ==="
            npm test -- --watchAll=false

            echo "=== Build Project ==="
            npm run build

            echo "=== Check Build Folder ==="
            ls -la build

            echo "=== Check index.html ==="
            test -f build/index.html
        '''
            }
        }
    
    }


}
