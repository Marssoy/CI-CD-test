pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        BUCKET_NAME = 'marssoycloud.com.br'
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
    }

    stage('Upload to S3') {
        steps {
            script {
                sh '''
                aws s3 sync . s3://${BUCKET_NAME}/ --region ${AWS_REGION} --execute "*.git/*"
                '''
            }
        }
    }
}