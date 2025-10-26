pipeline {
    agent any

    environment {
        PYTHON = "C:\\Users\\tanuj\\AppData\\Local\\Microsoft\\WindowsApps\\python.exe"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Extract Data') {
            steps {
                bat "${env.PYTHON} extract_1.py"
            }
        }
    }

    post {
        success {
            echo "Task success ..."
        }
        failure {
            echo "Task failure ..."
        }
    }
}
