pipeline {
    agent any

    environment {
        // 设置环境变量，如Maven和Docker相关配置
        MAVEN_OPTS = '-Dmaven.repo.local=$WORKSPACE/.m2/repository'
        IMAGE_NAME = 'jenkins-test/xxl-job'
        TAG = 'latest'
        REGISTRY_URL = 'http://100.98.100.234'
        DOCKER_CREDENTIAL_ID = '234-harbor' // Harbor的凭证ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', credentialsId: 'github-credent', url: 'https://github.com/1056661516/xxl-job.git'
            }
        }
        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }
        stage('Push to Harbor') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIAL_ID}", passwordVariable: 'HARBOR_PASSWORD', usernameVariable: 'HARBOR_USERNAME')]) {
                    sh "docker login -u ${HARBOR_USERNAME} -p ${HARBOR_PASSWORD} ${REGISTRY_URL}"
                    docker.withRegistry("${REGISTRY_URL}", 'harbor-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}