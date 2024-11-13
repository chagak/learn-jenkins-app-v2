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
                    ls -lart
                '''
            }
        }
        stage ('"Test"') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Test stage"
                    if [ -f /build/index.html ]; then
                            echo "File exists."
                        else
                            echo "File does not exist."
                        fi
                    npm test
                '''
            }
        }
        stage ('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install -g serve
                    serve -s build
                    npx playwright test
                '''
            }
        }
    }
    post {
        always {
            // test-result directory is not in the working directory
            //junit 'test-result/junit.xml'
        }
    }
}
}