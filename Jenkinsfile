pipeline {
    agent any // Выбираем Jenkins агента, на котором будет происходить сборка: нам нужен любой

    stages {
        stage('Check User Environment Variables') {
            steps {
                script {
                    // Выводим все переменные, связанные с пользователем сборки
                    echo "BUILD_USER_ID: ${env.BUILD_USER_ID}"
                    echo "BUILD_USER_FIRST_NAME: ${env.BUILD_USER_FIRST_NAME}"
                    echo "BUILD_USER_LAST_NAME: ${env.BUILD_USER_LAST_NAME}"
                    echo "BUILD_USER_GROUPS: ${env.BUILD_USER_GROUPS}"
                    echo "BUILD_USER_EMAIL: ${env.BUILD_USER_EMAIL}"
                }
            }
        }
    }
}
