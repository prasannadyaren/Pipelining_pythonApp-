pipeline {
    agent any

    environment {
        VENV = "venv"
        // Quoted path because of the space in your username
        PYTHON = "\"C:\\Users\\Lakshmi prasanna\\AppData\\Local\\Programs\\Python\\Python313\\python.exe\""
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
                bat ".\\%VENV%\\Scripts\\python.exe -m pip install --upgrade pip"
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
