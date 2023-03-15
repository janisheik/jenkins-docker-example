pipeline{
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('valaxy-maven-deploy')
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/janisheik/jenkins-docker-example.git']])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t jani180348/my-app-1.0:latest .'
                }
            }
        }
        stage('login and push image') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push jani180348/my-app-1.0:latest'
            }
        }   
    }
}
