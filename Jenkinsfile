pipeline {
    agent any

    environment {
        NODE_IMAGE = 'node:18-alpine'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image "${env.NODE_IMAGE}"
                    reuseNode true
                }
            }

            steps {
                sh '''
                    echo "Building the application"
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image "${env.NODE_IMAGE}"
                    reuseNode true
                }
            }

            steps {
                sh '''
                    echo "Running tests"
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }

    post {
        always {
            echo 'This will always run'
            junit 'test-results/junit.xml'
        }
    }
}
