pipeline {
    agent any

    environment {

        credentialsId = "google-application-credentials"     
        project = "dev-melon-fan-platform-project"
        bucket = "dev-melon-fan-platform-kor-bucket"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Store to GCS') {
            steps{
                step([
                        $class: 'ClassicUploadStep', 
                        credentialsId: ${credentialsId},  
                        bucket: "gs://${bucket}/swagger_test/melon-fan-lounge",
                        pattern: "**/api-spec.yml"
                    ])
            }
        }
    }
}