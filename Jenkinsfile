pipeline {
    agent any
    stages {
        stage('Get Branch Info') {
            steps {
                script {
                    // 获取当前构建所基于的Git分支名称
                    def branchName = env.BRANCH_NAME
                    echo "Current branch: ${branchName}"
                }
            }
        }
    }
}
