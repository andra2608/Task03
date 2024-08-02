pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/andra2608/Task03.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.image('python:3.8').inside {
                        sh 'pip install -r requirements.txt'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('python:3.8').inside {
                        sh 'python -m unittest discover'
                    }
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/test-results.xml', allowEmptyArchive: true
            junit 'test-results.xml'
        }
        success {
            mail to: 'dileep.andra12@gmail.com',
                 subject: "SUCCESS: Build ${env.BUILD_NUMBER}",
                 body: "Good job! The build succeeded."
        }
        failure {
            mail to: 'dileep.andra12@gmail.com',
                 subject: "FAILURE: Build ${env.BUILD_NUMBER}",
                 body: "Oops! The build failed."
        }
    }
}
