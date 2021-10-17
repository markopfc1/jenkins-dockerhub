pipeline {
    agent { label 'master' }
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-markopfc1')
    }

    stages {

        stage('Checkout') {
            steps{
                git branch: 'main', url: 'git@github.com:markopfc1/jenkins-dockerhub.git'
            }
        }

        stage('Build') {
            steps{
                sh 'docker build -t devops14:latest .'
            }
        }

        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('ImageTag') {
            steps {
                sh 'docker tag devops14:latest markopfc1/devops14-docker:version2'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push markopfc1/devops14-docker:version2'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
