
pipeline {
    agent any

    stages {
        stage('Welcome') {
            steps {
                echo 'Welcome to DevOps!'
            }
        }

        stage('Create Website') {
            steps {
                sh '''
                    set -eu

                    mkdir -p xyz

                    cat > xyz/index.html <<'EOF'
                    <!DOCTYPE html>
                    <html>
                    <head>
                        <title>Welcome to DevOps</title>
                    </head>
                    <body>
                        <h1>Welcome to DevOps!</h1>
                        <p>Website created using Jenkins Pipeline.</p>
                    </body>
                    </html>
                    EOF

                    echo "Website created successfully."
                '''
            }
        }

        stage('Test Website') {
            steps {
                sh '''
                    test -f xyz/index.html
                    grep -q "Welcome to DevOps!" xyz/index.html
                    echo "Website test passed!"
                '''
            }
        }

        stage('Archive Website') {
            steps {
                archiveArtifacts artifacts: 'xyz/**',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
