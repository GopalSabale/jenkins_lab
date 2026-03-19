pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
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
    }
}