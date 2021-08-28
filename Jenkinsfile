pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //sh - Mac bat -Windows
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                //bat - for windows , sh - for Mac
                sh "docker build -t='raghavkj/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    //sh
                    sh "docker login --username=${user} --password=${pass}"
                    sh "docker push raghavkj/selenium-docker:latest"
                }
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}