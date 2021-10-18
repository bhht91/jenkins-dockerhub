pipeline {
    agent { label 'master' }
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-burhan')
    }

    stages {

        stage('Checkout') {
            steps{
                git branch: 'main', url: 'git@github.com:bhht91/jenkins-dockerhub.git'
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
                sh 'docker tag devops14:latest bhht91/devops14-docker:version1'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push bhht91/devops14-docker:version1'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
            if (getContext(hudson.FilePath)) {
                    deleteDir()
                }
        }
    }
}
