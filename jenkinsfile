pipeline {
    agent any

    environment {
        // Python environment variable
        PYTHON = "C:\\Users\\tanuj\\AppData\\Local\\Microsoft\\WindowsApps\\python.exe"
    }

    stages {
        // Stage 1: Checkout code
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        // Stage 2: Run Python script
        stage('Run Python Script') {
            steps {
                bat "${env.PYTHON} extract_1.py"
            }
        }

        // Stage 3: Build with Maven
        stage('Build with Maven') {
            steps {
                // Only wrap Maven build inside withMaven
                withMaven(maven: 'M3') {
                    sh 'mvn clean install'
                }
            }
        }

        // Stage 4: Trigger downstream pipeline safely
        stage('Trigger Downstream Pipeline') {
            steps {
                // Trigger downstream job and wait until it completes
                build job: 'extract_pipeline_2', wait: true
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs for details."
        }
    }
}
