pipeline {
    agent any
    options {
        withBuildUser()
    }
    stages {
        stage('Build') {
            steps {
                script {
                    echo "The build was triggered by user: ${env.BUILD_USER_ID}"
                }
            }
        }
    }
}
