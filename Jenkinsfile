pipeline {
    agent {
        label 'jawwad'
    }

    stages {

        stage('Code Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Jawwad-codes/django-notes-app.git'
            }
        }
        
        stage('Docker Build image') {
            steps {
                sh '''
                    echo "======Build Images======"
                    docker build -t notes-app:latest .
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
         stage('Push Image To Docker Hub') {
            steps {
                sh '''
                    echo "========PUSH THE IMAGE OF NOTES APP TO DOCKER HUB========"
                    docker login
                    docker image tage notes-app:latest jawwadnadeem/notes-app:latest
                    docker push jawwadnadeem/notes-app:latest
                '''
            }
        }

        stage('Docker Compose Up') {
            steps {
                sh '''
                    echo "===== STARTING APPLICATION ====="

                    docker-compose up -d
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
