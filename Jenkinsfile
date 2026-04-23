pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repository...'
            }
        }
        stage('Build') {
            steps {
                dir('java-maven') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
        stage('Test') {
            steps {
                dir('java-maven') {
                    sh 'mvn test'
                }
            }
        }
        stage('Docker Build') {
            steps {
                dir('java-maven') {
                    sh 'docker build -t medox2003/java-maven:latest .'
                }
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHub',
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                    sh 'docker push medox2003/java-maven:latest'
                }
            }
        }
    }
}
