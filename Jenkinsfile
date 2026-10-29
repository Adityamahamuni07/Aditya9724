
pipeline {
    agent any

    stages {

        stage('Welcome') {
            steps {
                echo 'Welcome to Jenkins CI/CD!'
            }
        }

        stage('Checkout') {
            steps {
                echo 'Source code is available in the workspace.'
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mkdir -p build
                    echo "Build successful!" > build/result.txt
                    cat build/result.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    test -s build/result.txt
                    grep -q "Build successful!" build/result.txt
                    echo "All tests passed!"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
