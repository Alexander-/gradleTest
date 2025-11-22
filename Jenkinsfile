pipeline {
    echo "set agent to any"
    agent any


    stages {
        stage('Build') {
            echo "start Build stage"
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
            echo "test results"
            junit testResults: '**/build/test-results/test/*.xml',
                  allowEmptyResults: true
        }
    }
}