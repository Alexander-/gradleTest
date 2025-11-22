pipeline {
    sh "set agent to any"
    agent any


    stages {
        stage('Build') {
            sh "start Build stage"
            steps {
                sh './gradlew clean build'
            }
        }
    }

    post {
        always {
            // Сохраняем JAR-файлы
            archiveArtifacts artifacts: '**/build/libs/*.jar',
                             allowEmptyArchive: true,
                             fingerprint: true

            // Публикуем результаты тестов (если они есть)
            sh "test results"
            junit testResults: '**/build/test-results/test/*.xml',
                  allowEmptyResults: true
        }
    }
}