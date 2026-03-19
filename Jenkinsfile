pipeline {
    agent any

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
                echo 'creating the docker container'
                sh 'docker container run -d --name c1 nginx'
                echo 'container has been completed'
            }
        }
        stage('create a image from running container') {
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
    }
}


