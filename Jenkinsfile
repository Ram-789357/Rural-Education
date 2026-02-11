pipeline {
    agent any

    stages {

        stage('Checkout SCM') {
            steps {
                git branch: 'main',
                credentialsId: 'github-creds',
                url: 'https://github.com/Ram-789357/Rural-Education.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t rural-learn-site .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker rm -f rural-container || exit 0'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8098:80 --name rural-container rural-learn-site'
            }
        }
    }

    post {
        success {
            echo 'Website is LIVE at http://localhost:8085'
        }
    }
}
