pipeline {
    agent any

    stages {
        /*stage('Build') {
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
        }*/
        
        stage('Test') {  // Removed quotes around the stage name
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Test stage"
                    if [ -f build/index.html ]; then
                        echo "File exists."
                    else
                        echo "File does not exist."
                    fi
                    npm test
                '''
            }
        }
        
        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    sudo npm install -g serve
                    sudo serve -s build
                    sudo npx playwright test
                '''
            }
        }
    }
    
    post {
        always {
            echo "test-result directory is not in the working directory"
            // Uncomment and correct the path if JUnit files are expected
            // junit 'test-result/junit.xml'
        }
    }
}
