pipeline {
    agent any

    environment {
        // 환경 변수로 Credential ID 지정
        GOOGLE_APPLICATION_CREDENTIALS = credentials('GOOGLE_APPLICATION_CREDENITALS')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Authenticate with GCP') {
            steps {
                script {
                    // gcloud 명령어를 사용하여 인증
                    sh "gcloud auth activate-service-account --key-file=${env.GOOGLE_APPLICATION_CREDENTIALS}"
                }
            }
        }

        stage('Upload to GCS') {
            steps {
                script {
                    // Set environment variables or use Jenkins credentials
                    
                    sh '''
                    gcloud config set dev-melon-fan-platform-project

                    # Upload files to GCS
                    gsutil cp admin-api/api-spec.yml dev-melon-fan-platform-kor-bucket/leo-test/admin-api/api-spec.yml
                    gsutil cp rest-api/api-spec.yml dev-melon-fan-platform-kor-bucket/leo-test/rest-api/api-spec.yml
                    '''
                }
            }
        }
    }
}