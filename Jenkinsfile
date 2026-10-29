
pipeline {
    agent any

    environment {
        APP_NAME = 'DevOpsCompany'
        BUILD_DIR = 'website'
    }

    stages {

        stage('Welcome') {
            steps {
                echo 'Starting DevOps Website Pipeline'
            }
        }

        stage('Check Environment') {
            steps {
                sh '''
                    echo "Application: $APP_NAME"
                    echo "Build Number: $BUILD_NUMBER"
                    echo "Workspace: $WORKSPACE"
                    echo "Checking Linux environment..."
                    pwd
                    ls -la
                '''
            }
        }

        stage('Create Website') {
            steps {
                sh '''
                    mkdir -p "$BUILD_DIR"

                    cat > "$BUILD_DIR/index.html" <<'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">
    <title>DevOps Company</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: #eef2ff;
            padding: 60px 20px;
        }
        h1 {
            color: #174ea6;
        }
        .card {
            background: white;
            padding: 30px;
            margin: auto;
            max-width: 600px;
            border-radius: 12px;
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>Welcome to DevOps Company!</h1>
        <p>Built automatically using Jenkins Pipeline.</p>
        <p>Tools: GitHub, Jenkins, Docker and AWS.</p>
        <p>Status: Website build successful.</p>
    </div>
</body>
</html>
EOF

                    echo "Website files created."
                '''
            }
        }

        stage('Test Website') {
            steps {
                sh '''
                    test -f "$BUILD_DIR/index.html"
                    grep -q "Welcome to DevOps Company!" \
                        "$BUILD_DIR/index.html"
                    grep -q "Jenkins Pipeline" \
                        "$BUILD_DIR/index.html"

                    echo "All website tests passed!"
                '''
            }
        }

        stage('Build Report') {
            steps {
                sh '''
                    {
                        echo "Application: $APP_NAME"
                        echo "Build Number: $BUILD_NUMBER"
                        echo "Build Date: $(date)"
                        echo "Result: SUCCESS"
                    } > "$BUILD_DIR/build-report.txt"

                    cat "$BUILD_DIR/build-report.txt"
                '''
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'website/**',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Website built and archived!'
        }

        failure {
            echo 'FAILURE: Check the Console Output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
