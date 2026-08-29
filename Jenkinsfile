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

        stage('Docker Compose Down') {
            steps {
                sh '''
                    echo "===== STOPPING OLD CONTAINERS ====="

                    docker-compose down || true
                '''
            }
        }
         stage('Docker Build') {
            steps {
                sh '''
                    echo "===== STARTING APPLICATION ====="
                    docker images
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
