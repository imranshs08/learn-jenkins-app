pipeline {
    agent any 

    stages {
        // This is a comment
        /*
        line 1
        line 2
        */
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    clearWs()
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
             agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Test stage"
                    test build/index.html
                    npm test
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