pipeline {
    agent any  // 어떤 환경에서든 실행

    environment {
        MY_VARIABLE = "some-value"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                // 빌드 명령 실행
                sh 'make'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                // 테스트 명령 실행
                sh 'make test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying..'
                // 배포 명령 실행
                sh 'make deploy'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    }
}