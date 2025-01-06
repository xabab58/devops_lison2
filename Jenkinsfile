pipeline {
    agent any // Выбираем Jenkins агента, на котором будет происходить сборка: нам нужен любой

    stages {
        stage('Check Environment Variables') {
            steps {
                script {
                    // Выводим значение переменной окружения, которая может быть ответственной за сборщика
                    echo "BUILD_USER_ID: ${env.BUILD_USER_ID}"  // Проверяем переменную BUILD_USER_ID
                    echo "GIT_COMMITTER_NAME: ${env.GIT_COMMITTER_NAME}"  // Проверяем переменную GIT_COMMITTER_NAME
                    echo "USER: ${env.USER}"  // Также проверим переменную USER, которая может быть полезна
                }
            }
        }
    }
}
