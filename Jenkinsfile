pipeline {
    agent any // Выбираем Jenkins агента, на котором будет происходить сборка: нам нужен любой

    triggers {
        pollSCM('H/5 * * * *') // Запускать будем автоматически по крону примерно раз в 5 минут
    }

    tools {
        maven 'maven-3.8.1' // Для сборки бэкенда нужен Maven
        jdk 'jdk16' // И Java Developer Kit нужной версии
        nodejs 'node-16' // А NodeJS нужен для фронта
    }

    stages {
        stage('Build & Test backend') {
            steps {
                dir("backend") { // Переходим в папку backend
                    sh 'mvn package' // Собираем мавеном бэкенд
                }
            }

            post {
                success {
                    junit 'backend/target/surefire-reports/**/*.xml' // Передадим результаты тестов в Jenkins
                }
            }
        }

        stage('Build frontend') {
            steps {
                dir("frontend") {
                    sh 'npm install' // Для фронта сначала загрузим все сторонние зависимости
                    sh 'npm run build' // Запустим сборку
                }
            }
        }
        
        stage('Save artifacts') {
            steps {
                archiveArtifacts(artifacts: 'backend/target/sausage-store-0.0.1-SNAPSHOT.jar')
                archiveArtifacts(artifacts: 'frontend/dist/frontend/*')
            }
        post {
                success {
                    script {
                        // URL вашего Telegram-бота (замените на свой)
                        def telegramApiUrl = 'https://api.telegram.org/bot5310374541:AAFJdesNVXobebUtvGbbLPJr800r256uYw4/sendMessage'
                        // ID вашего Telegram-канала (замените на свой)
                        def chatId = '-4667291640'
                        // Формируем сообщение для отправки
                        def user = env.BUILD_USER_ID ?: 'Неизвестный пользователь'

                        def message = "Сборка приложения успешно завершена!\n" +
                                    "Имя сборки: ${env.JOB_NAME}\n" +
                                    "Ссылка на результаты: ${env.BUILD_URL}\n" +
                                    "Сборщик: ${user}"

                        // Отправляем запрос в Telegram
                        sh """
                            curl -X POST ${telegramApiUrl} -d chat_id=${chatId} -d text="${message}"
                        """
                        echo "Сборщик: ${env.BUILD_USER_ID}"
                    }
                }
            }
        }
    }
}