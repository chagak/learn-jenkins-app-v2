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
        stage ("Test") {
            steps {
                sh '''
                    echo "Test stage"
                    if [ -f /path/to/directory/filename ]; then
                            echo "File exists."
                        else
                            echo "File does not exist."
                        fi

                '''
            }
        }
    }
}