pipeline {
    agent any

    tools {
        maven "MAVEN3"
    }

    environment {
        DOCKERHUB_PWD = credentials('CredentialID_DockerHubPWD')
    }

    stages {
        stage('Check out') {
            steps {
                git branch: 'main', url: 'https://github.com/rbudha05/maven-docker-jenkins-lab.git'
            }
        }

        stage('Build maven project') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Docker login') {
            steps {
                bat 'docker login -u rohit050201 -p %DOCKERHUB_PWD%'
            }
        }

        stage('Docker build') {
            steps {
                bat 'docker build -t rohit050201/mavenproject:1.0 .'
            }
        }

        stage('Docker push') {
            steps {
                bat 'docker push rohit050201/mavenproject:1.0'
            }
        }
    }
}
