pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                script {
                    try {
                        sh '''
                            ls -la
                            node --version
                            npm --version
                            npm ci
                            npm run build
                            ls -la
                        '''
                    } catch(Exception e) {
                        throw new Exception("Build stage failed: ${e.getMessage()}")
                    }
                }
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
                script {
                    try {
                        sh '''
                            test -f build/index.html
                            ls -la
                            npm run test
                            ls -la
                        '''
                    } catch(Exception e) {
                        throw new Exception("Test stage failed: ${e.getMessage()}")
                    }
                }
                sh '''
                    test -f build/index.html
                    ls -la
                    npm run test
                    ls -la
                '''
            }
        }
    }
}
