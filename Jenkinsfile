pipeline {

    agent {
        label 'frontend-agent'
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
                    test -f script.js

                    echo "All required frontend files are present."
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building frontend application...'

                sh '''
                    mkdir -p build
                    cp index.html build/
                    cp style.css build/
                    cp script.js build/

                    echo "Frontend build completed."
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying frontend application...'

                sh '''
                    mkdir -p /home/cselab8/jenkins-agent/deployed-app

                    cp build/index.html /home/cselab8/jenkins-agent/deployed-app/
                    cp build/style.css /home/cselab8/jenkins-agent/deployed-app/
                    cp build/script.js /home/cselab8/jenkins-agent/deployed-app/

                    echo "Frontend deployed successfully."
                '''
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
