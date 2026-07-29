pipeline {
    agent any
    stages {
        stage('build') {
              
            steps {
             
                sh '''
                    echo "trying pipeline build with github"
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
                    test -f build/index.html
                    npm test
                   
                    '''
            }
        }
    }
    post {
        always {
            echo 'This will always run'
            JUnit test results will be published in the Jenkins console output.
            jUnit  'test-results/junit.xml'       
    }
}
