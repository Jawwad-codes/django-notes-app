pipeline {
    agent {
        label 'jawwad'
    }

    stages {

        stage('Code Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Jawwad-codes/django-notes-app.git'

                sh '''
                    echo "===== CODE CLONED ====="
                    whoami
                '''
            }
        }

        stage('Install Docker Compose') {
            steps {
                sh '''
                    echo "===== INSTALLING DOCKER COMPOSE ====="

                    sudo apt-get update
                    sudo apt-get install -y docker-compose

                    echo "===== DOCKER VERSION ====="
                    docker --version

                    echo "===== DOCKER COMPOSE VERSION ====="
                    docker compose version
                '''
            }
        }

        stage('Docker Compose Down') {
            steps {
                sh '''
                    echo "===== STOPPING OLD CONTAINERS ====="

                    docker-compose down || true
                '''
            }
        }

        stage('Docker Compose Build') {
            steps {
                sh '''
                    echo "===== BUILDING DOCKER IMAGE ====="

                    docker-compose build
                '''
            }
        }

        stage('Docker Compose Up') {
            steps {
                sh '''
                    echo "===== STARTING APPLICATION ====="

                    docker-compose up -d

                    echo "===== RUNNING CONTAINERS ====="
                    docker-compose ps
                '''
            }
        }
    }

    post {
        success {
            echo '===== CI/CD SUCCESS ====='
        }

        failure {
            echo '===== CI/CD FAILED ====='
        }
    }
}
