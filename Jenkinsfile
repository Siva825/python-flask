pipeline {
    agent any
       
    stages{
        stage ('Cloning repository'){
            steps {
                git 'https://github.com/Siva825/python-flask.git'
            }   
        }
        stage ('Building python image'){
            steps {
                dir('python-flask/python'){
                    sh 'docker build -t siva2626/python_image:latest .'
                }
            }
        }
        stage ('Building java image'){
            steps {
                dir('python-flask/java'){
                    sh 'docker build -t siva2626/java_image:latest .'
                }
            }
        }
        stage ('Building nginx image'){
            steps {
                dir('python-flask/nginx'){
                    sh 'docker build -t  siva2626/nginx_image:latest .'
                }
            }
        }
        stage ('Pushing images to Docker Hub'){
             environment {
            DOCKERHUB_CREDENTIALS = credentials('docker-creds')
        }
            steps {
               
                    sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
                    sh 'docker push siva2626/python_image:latest'
                    sh 'docker push siva2626/java_image:latest'
                    sh 'docker push siva2626/nginx_image:latest'
                
            }
        }
    }
}
 
