pipeline {
    agent any

    environment {
        // 환경 변수로 Credential ID 지정
        // GOOGLE_APPLICATION_CREDENTIALS = credentials('GOOGLE_APPLICATION_CREDENITALS')
        project = "dev-melon-fan-platform-project"
        bucket = "dev-melon-fan-platform-kor-bucket"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage("set gcloud, gsutil"){
            steps{
                sh("""export PATH="$HOME/gcloud-sdk/bin:$PATH" """)
                
            }
        }

        stage('Authenticate with GCP') {
            steps {
                withCredentials([file(credentialsId: 'GOOGLE_APPLICATION_CREDENITALS', variable: 'GOOGLE_APPLICATION_CREDENITALS')]) {
                    sh("gcloud auth activate-service-account --key-file=${GOOGLE_APPLICATION_CREDENITALS}")
                    sh("gcloud config set ${project}")
                }

                // script {
                //     // gcloud 명령어를 사용하여 인증
                //     sh "gcloud auth activate-service-account --key-file=${env.GOOGLE_APPLICATION_CREDENTIALS}"
                // }
            }
        }

        stage('Upload to GCS') {
            steps {
                script {
                    // Set environment variables or use Jenkins credentials
                    
                    sh("gsutil cp admin-api/api-spec.yml ${bucket}/leo-test/admin-api/api-spec.yml")
                    sh("gsutil cp rest-api/api-spec.yml ${bucket}/leo-test/rest-api/api-spec.yml")
                    
                }
            }
        }
    }
}