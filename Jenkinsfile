pipeline {
    agent any

    environment {
        VENV = "venv"
        PYTHON = "C:\\Users\\Lakshmi prasanna\\AppData\\Local\\Programs\\Python\\Python310\\python.exe"
    }

    stages {
        stage('Clone GitHub Repo') {
            steps {
                git branch: 'main', credentialsId: 'github-https', url: 'https://github.com/prasannadyaren/Pipelining_pythonApp-.git'
            }
        }

        stage('Set Up Python Virtual Environment') {
            steps {
                bat '"%PYTHON%" -m venv %VENV%'
                bat '.\\%VENV%\\Scripts\\python.exe -m pip install --upgrade pip'
                bat '.\\%VENV%\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run Flask App in Background') {
            steps {
                bat '''
                start /B .\\%VENV%\\Scripts\\python.exe app.py
                echo Flask started at: http://localhost:5000/
                '''
            }
        }
    }

    post {
        always {
            echo 'Stopping Flask app...'
            // Kill Flask process after pipeline finishes
            bat 'for /f "tokens=5" %a in (\'netstat -ano ^| findstr :5000\') do taskkill /PID %a /F'
        }
    }
}
