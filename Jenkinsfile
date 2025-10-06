pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-username/cloudformation-deploy.git', credentialsId: 'github-token'
            }
        }

        stage('Validate Template') {
            steps {
                sh 'aws cloudformation validate-template --template-body file://template.yaml'
            }
        }

        stage('Deploy Stack') {
            steps {
                sh '''
                aws cloudformation deploy \
                    --template-file template.yaml \
                    --stack-name MyStack \
                    --capabilities CAPABILITY_NAMED_IAM
                '''
            }
        }
    }
}
