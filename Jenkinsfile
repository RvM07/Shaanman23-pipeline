pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/RvM07/Shaanman23-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Flask Docker Image..."
                    sh 'docker build -t flaskapp .'
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                if docker ps -q --filter "name=flaskapp-container"; then
                    docker stop flaskapp-container || true
                    docker rm flaskapp-container || true
                fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flaskapp-container flaskapp'
            }
        }

        stage('Test Application') {
            steps {
                sh 'curl -f http://localhost:5000'
            }
        }

        stage('Deploy Success') {
            steps {
                echo "Deployment Completed Successfully!"
            }
        }
    }
}
