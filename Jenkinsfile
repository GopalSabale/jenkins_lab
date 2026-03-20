pipeline {
    agent any
    environment {
        AWS_REGION=us-east-1
        ACCOUNT_ID=315354952103
        REPO_NAME=my-test_jenkins
        IMAGE_TAG=latest
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
    }

    tools {
        maven 'mvn_3.9.12'
    }

    environment {
        ENV = 'dev'
    }

    stages {

        stage('Code Compilations') {
            steps {
                echo 'Running the compilation'
                sh 'mvn clean compile'
                echo 'Maven compilation completed'
            }
        }

        stage('Code QA Test') {
            steps {
                echo 'Running JUnit tests'
                sh 'mvn test'
                echo 'Maven test completed'
            }
        }

        stage('Code Package') {
            steps {
                echo 'Packaging the code'
                sh 'mvn package'
            }
        }
        stage('create docker container') {
            steps {
                echo 'image is creating'
                sh '''
                if [ "$(docker container ps -a -q -f name=c1)" ]; then
                    echo 'docker container already exist....'
                else
                    docker container run -d --name c1 nginx
                fi
                '''
            }
        }
        stage('create a image from running container') {
            steps {
                echo 'creating the docker image from container'
                sh 'docker commit c1 c1_image:v1'
                echo 'image has been created'
            }
        }
        stage('login to ECR')
            steps {
                echo 'logging to ECR'
                sh 'aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com'
                echo 'login successfully'
            }
        }
    }
}


