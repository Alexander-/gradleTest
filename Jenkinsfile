pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                echo "start Build stage"
                sh 'chmod +x ./gradlew'
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
            junit testResults: '**/build/test-results/test/*.xml',
                  allowEmptyResults: true
        }
    }
}