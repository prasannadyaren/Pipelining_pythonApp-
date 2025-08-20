pipeline {
    agent any

    environment {
        VENV = "venv"
        // Use Python 3.10 path (quoted because of space in username)
        PYTHON = "\"C:\\Users\\Lakshmi prasanna\\AppData\\Local\\Programs\\Python\\Python310\\python.exe\""
    }

    stages {
        stage('Clone GitHub Repo') {
            steps {
                git branch: 'main', 
                    credentialsId: 'github-https', 
                    url: 'https://github.com/prasannadyaren/Pipelining_pythonApp-.git'
            }
        }

        stage('Set Up Python Virtual Environment') {
            steps {
                bat "${PYTHON} -m venv %VENV%"
                bat ".\\%VENV%\\Scripts\\python.exe -m pip install --upgrade pip setuptools wheel build"
                bat ".\\%VENV%\\Scripts\\pip install -r requirements.txt"
            }
        }

        stage('Run Flask App in Background') {
            steps {
                bat '''
                start /B .\\venv\\Scripts\\python.exe app.py
                '''
                echo "🚀 Flask app started in background"
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline finished successfully!"
        }
        failure {
            echo "❌ Pipeline failed! Please check logs."
        }
    }
}
