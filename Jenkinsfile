pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'd2227b9b-17ed-4d86-8419-cf0f79e3214c'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Hello World'
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

        stage('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }

                stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Hello World'
                sh '''
                    npm install netlify-cli
                    npm --version
                    "Deploying to production. Site ID: $NETLIFLY_SITE_ID"
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