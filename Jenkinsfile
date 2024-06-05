pipeline {
    agent any
     environment {
        GITHUB_CREDENTIALS = credentials('1016')
    }

    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/NUCESFAST/scd-final-lab-exam-faticoco.git', credentialsId: '1016'
            }
        }
        
        stage('Dependency Installation') {
            steps {
                bat 'npm install'
            }
        }
        
        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t fatima71459/auth ./Auth'
                    bat 'docker build -t fatima71459/classrooms ./Classrooms'
                    bat 'docker build -t fatima71459/client ./client'
                    bat 'docker build -t fatima71459/event-bus ./event-bus'
                    bat 'docker build -t fatima71459/post ./Post'
                }
            }
        }

        stage('Run Docker Images') {
            steps {
                script {
                    bat 'docker run -d fatima71459/auth'
                    bat 'docker run -d fatima71459/classrooms'
                    bat 'docker run -d fatima71459/client'
                    bat 'docker run -d fatima71459/event-bus'
                    bat 'docker run -d fatima71459/post'
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: '1008', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                        docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                        docker push fatima71459/auth
                        docker push fatima71459/classrooms
                        docker push fatima71459/client
                        docker push fatima71459/event-bus
                        docker push fatima71459/post
                    """
                }
            }
        }
    }
}
