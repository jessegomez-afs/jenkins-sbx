#!/usr/bin/env groovy
pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = "us-east-1"
    }
    
    stages {
        stage('Launch EC2 Instance and Deploy Web App') {
            steps {
                withCredentials([[
                    // Binding AWS credentials
                    # $class: 'AmazonWebServicesCredentialsBinding',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    credentialsId: 'aws-cred-manasa',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]])
                {
                    script {
                        
                        // Launches EC2 instance along with a user data script
                        def instance_id = sh(script: '''
                            aws ec2 run-instances \
                            --image-id ami-08b5b3a93ed654d19 \
                            --instance-type t2.micro \
                            --query Instances[0].InstanceId \
                            --output text
                        ''', returnStdout: true).trim()
                        
                        echo "Launched instance is: $instance_id"
                        
                        echo "Launched and Deployed successfully..."
                        
                    }
                }
            }
        }
    }
}
