pipeline {
    agent any
    tools {
        maven 'maven3.8' // 引用你在全局配置中设置的Maven名称
    }

    environment {
        // 设置环境变量，如Maven和Docker相关配置
        //MAVEN_OPTS = "-Dmaven.repo.local=${workspace}/.m2/repository"
        IMAGE_NAME = 'chinapopin.com:18443/k8s/xxl-job'
        TAG = 'latest'
        REGISTRY_URL = 'https://chinapopin.com:18443/'
        DOCKER_CREDENTIAL_ID = '234harbor' // Harbor的凭证ID
    }

    
    stage('Execute K8s Command') {
        steps {
            echo "${branch}"
        }
    }
    
    }
