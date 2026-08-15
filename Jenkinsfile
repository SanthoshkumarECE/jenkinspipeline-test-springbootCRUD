pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
    }

    stages {

        stage('Maven Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t sandy1602/student-crud:latest .'
            }
        }

        stage('Push image to Hub') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'DockerPwd',
                        variable: 'DockerPwd'
                    )
                ]) {
                    bat 'docker login -u sandy1602 -p %DockerPwd%'
                    bat 'docker push sandy1602/student-crud:latest'
                }
            }
        }
    }
}