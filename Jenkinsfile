pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-creds')
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Images in Parallel') {
            parallel {
                stage('Build Python Image') {
                    steps {
                        dir('python') {
                            sh 'docker build -t siva2626/python_image1:v2 .'
                        }
                    }
                }
                
                stage('Build Java Image') {
                    steps {
                        dir('java') {
                            sh 'docker build -t siva2626/java_image1:v2 .'
                        }
                    }
                }
                
                stage('Build Nginx Image') {
                    steps {
                        dir('nginx') {
                            sh 'docker build -t siva2626/nginx_image1:v2 .'
                        }
                    }
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh """
                    docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
                    docker push siva2626/python_image1:v2
                    docker push siva2626/java_image1:v2
                    docker push siva2626/nginx_image1:v2
                """
            }
        }
    }
}
