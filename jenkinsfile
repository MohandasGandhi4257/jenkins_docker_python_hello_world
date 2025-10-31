pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'hello-world-python:1.0'
    }

    stages {

        stage('Checkout') {
            steps {
                echo '🔄 Checking out source code...'
                git branch: 'main', url: 'https://github.com/MohandasGandhi4257/jenkins_docker_python_hello_world.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    echo '🛠️  Building Docker image...'
                    if (fileExists('Dockerfile')) {
                        sh "docker build -t ${env.DOCKER_IMAGE} ."
                    } else {
                        error "❌ Dockerfile not found in workspace!"
                    }
                }
            }
        }

        stage('Docker Run') {
            steps {
                script {
                    echo '▶️ Running Docker container...'
                    sh "docker run -i --rm ${env.DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Python application Docker image built and run successfully!'
        }
        failure {
            echo '❌ Docker build or run failed.'
        }
        always {
            echo '🧹 Cleaning workspace...'
            cleanWs()
        }
    }
}

