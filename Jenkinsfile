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

        stage('Upload to S3') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'vmarssoy'
                ]]) {
                    script {
                        sh '''
                        aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                        aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                        aws s3 sync . s3://${BUCKET_NAME}/ --region ${AWS_REGION} --exclude "*.git/*"
                        '''
                    }
                }
            }
        }
    }
}