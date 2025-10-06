pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-credentials')
        AWS_SECRET_ACCESS_KEY = credentials('aws-credentials')
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sanit-Wasnik/cloudformation-deploy.git', credentialsId: 'github-token'
            }
        }

        stage('Validate Template') {
            steps {
                bat 'aws cloudformation validate-template --template-body file://template.yaml'
            }
        }

        stage('Deploy Stack') {
            steps {
                bat '''
                aws cloudformation deploy ^
                    --template-file template.yaml ^
                    --stack-name MyStack ^
                    --capabilities CAPABILITY_NAMED_IAM
                '''
            }
        }
    }

    post {
        success {
            echo '✅ CloudFormation stack deployed successfully!'
        }
        failure {
            echo '❌ Deployment failed. Check logs for details.'
        }
    }
}