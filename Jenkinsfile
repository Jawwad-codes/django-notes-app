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
                    docker buildx build -t notes-app:latest .
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
                echo "===========PUSH IMAGE TO DOCKER HUB============"
                withCredentials([usernamePassword('credentialsId':"jenkins",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag notes-app:latest jawwadnadeem/notes-app:latest"
                    sh "docker push jawwadnadeem/notes-app:latest"
                }
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
            echo '===== CI/CD SUCCESS COMPLETE ====='
        }

        failure {
            echo '===== CI/CD FAILED ====='
        }
    }
}
