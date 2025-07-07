pipeline {
    agent any

    environment {
        BUCKET_NAME = 'static-site-614543684417-ap-south-1-static-site-stack'
        CLOUDFRONT_DIST_ID = 'E30QMJCR57A5EE' // Replace with your actual CloudFront ID
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git 'https://github.com/Yuvanesh-Ram/static-site-cicd.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                export PATH=$PATH:/usr/local/bin
                aws s3 sync static-site/ s3://$BUCKET_NAME --delete
                '''
            }
        }

        stage('Invalidate CloudFront Cache') {
            steps {
                sh '''
                export PATH=$PATH:/usr/local/bin
                aws cloudfront create-invalidation --distribution-id $CLOUDFRONT_DIST_ID --paths "/*"
                '''
            }
        }
    }
}

