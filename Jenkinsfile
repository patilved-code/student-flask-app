pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Test Application') {
            steps {
                bat 'python -m py_compile app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"C:\\Users\\STUDENT.LAB5-DESKTOP-8.000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t student-flask-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '"C:\\Users\\STUDENT.LAB5-DESKTOP-8.000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" stop student-app || exit /b 0'
                bat '"C:\\Users\\STUDENT.LAB5-DESKTOP-8.000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" rm student-app || exit /b 0'
            }
        }

        stage('Deploy Application') {
            steps {
                bat '"C:\\Users\\STUDENT.LAB5-DESKTOP-8.000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" run -d -p 5000:5000 --name student-app student-flask-app'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"C:\\Users\\STUDENT.LAB5-DESKTOP-8.000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" ps'
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully using Jenkins.'
        }

        failure {
            echo 'Application deployment failed.'
        }
    }
}