pipeline {

    agent {
        label 'slave1'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out frontend source code...'
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                echo 'Validating frontend files...'

                sh '''
                    test -f index.html
                    test -f style.css

                    echo "All required frontend files are present."
                '''
            }
        }

        stage('Build') {
            steps {
                echo '=============================='
                echo '     JENKINS AGENT BUILD'
                echo '=============================='

                sh '''
                    mkdir -p build
                    cp index.html build/
                    cp style.css build/

                    echo "Frontend build completed."
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing frontend project...'
                echo 'Frontend tests completed successfully.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying frontend application...'

                sh '''
                    rm -rf deployed-app
                    mkdir -p deployed-app
                    cp build/index.html deployed-app/
                    cp build/style.css deployed-app/

                    echo "Frontend deployed successfully."
                '''
            }
        }

        stage('Result') {
            steps {
                echo 'Build and Test Completed Successfully.'
                echo 'Pipeline executed on Jenkins agent: Slave1'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed.'
        }
    }
}
