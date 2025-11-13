//In a single branch, there are three Dockerfiles
//for Java, Python, and Nginx. The Docker images must be created simultaneously
//for all three (Python, Java, and Nginx) and pushed to Docker Hub using Jenkins.

pipeline {
    agent any
       
    stages{
        stage ('Cloning repository'){
            steps {
               sh 'rm -rf python-flask || true'
               sh ' git clone https://github.com/Siva825/python-flask.git'
            }   
        }
        stage ('Building python image'){
            steps {
                dir('python-flask/python'){
                    sh 'sudo docker build -t siva2626/python_image:latest .'
                }
            }
        }
        stage ('Building java image'){
            steps {
                dir('python-flask/java'){
                    sh 'sudo docker build -t siva2626/java_image:latest .'
                }
            }
        }
        stage ('Building nginx image'){
            steps {
                dir('python-flask/nginx'){
                    sh 'sudo docker build -t  siva2626/nginx_image:latest .'
                }
            }
        }
        stage ('Pushing images to Docker Hub'){
             environment {
            DOCKERHUB_CREDENTIALS = credentials('docker-creds')
        }
            steps {
            // deleting all existing images if any build fails if only it fails dont need error for first time
                    sh 'sudo docker image prune -f|| true'
                    sh 'sudo docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
                    sh 'sudo docker push siva2626/python_image:latest'
                    sh 'sudo docker push siva2626/java_image:latest'
                    sh 'sudo docker push siva2626/nginx_image:latest'
                
            }
        }
    }
}
 

