pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/eligetipavankumar/multi-stage-example.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("pavankumar03032001/myapp:latest")
                }
            }
        }

        stage('Login to DockerHub and Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-cred') {
                        def dockerImage = docker.image("pavankumar03032001/myapp:latest")
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Docker image pushed to Docker Hub successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
