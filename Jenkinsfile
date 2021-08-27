pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //bat
                sh "mvn clean package -DskipTests"
            }
        }
        environment {
          DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        }

        stage('Build Image') {
            steps {
                //bat
                sh 'docker build -t raghavkjdocker/selenium-docker:latest .'
            }
        }
        stage('Login') {
          steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          }
        }
        stage('Push Image') {
          steps {
			sh 'docker push raghavkjdocker/selenium-docker:latest'
		  }
        }
        post {
          always {
            sh 'docker logout'
          }
        }
    }
  }