pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    // Используем withBuildUser внутри блоков node
                    withBuildUser {
                        def user = env.BUILD_USER_ID
                        echo "Build triggered by user: ${user}"
                    }
                }
            }
        }
    }
}
