
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
                    mkdir -p xyz

                    cat > xyz/index.html <<'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to DevOps</title>
    <style>
        body {
            background-color: #101827;
            color: white;
            font-family: Arial, sans-serif;
            text-align: center;
            padding-top: 100px;
        }
        h1 {
            color: #00e5a8;
        }
    </style>
</head>
<body>
    <h1>Welcome to DevOps!</h1>
    <p>My website is created using Jenkins Pipeline.</p>
    <p>Learning AWS, Linux, Git, Docker and CI/CD.</p>
</body>
</html>
EOF

                    echo "Website created successfully!"
                '''
            }
        }

        stage('Test Website') {
            steps {
                sh '''
                    test -s xyz/index.html
                    grep -q "Welcome to DevOps!" xyz/index.html

                    echo "Website test passed!"
                '''
            }
        }

        stage('Archive Website') {
            steps {
                archiveArtifacts artifacts: 'xyz/index.html',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Welcome DevOps website pipeline completed!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
