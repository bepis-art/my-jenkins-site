pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Код скачан из GitHub!'
                sh 'ls -la' // Покажем файлы в логе
            }
        }

        stage('Build') {
            steps {
                echo '🏗️ Собираем Docker образ...'
                sh 'docker build -t my-website:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Обновляем контейнер...'
                sh 'docker stop my-website-container || true'
                sh 'docker rm my-website-container || true'
                sh 'docker run -d --name my-website-container -p 8081:80 my-website:latest'
            }
        }
        
        stage('Test') {
            steps {
                echo '✅ Проверяем работу...'
                sh 'sleep 2 && curl -I http://localhost:8081'
            }
        }
    }
    post {
        always {
            sh 'docker image prune -f'
        }
    }
}
