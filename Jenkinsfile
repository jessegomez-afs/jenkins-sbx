#!/usr/bin/env groovy
pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = "us-east-1"
        AWS_EXE = 'C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe'
    }
    
    stages {
        stage('alpha) {
            steps {
		echo 'alpha...'
                withCredentials([[
                    // Binding AWS Credentials
                    $class: 'AmazonWebServicesCredentialsBinding',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    credentialsId: 'aws-cred-manasa',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    script {
                        
                        // Launches EC2 instance along with a user data script
                        def instance_id = "${AWS_EXE} ec2 run-instances \
                            --image-id ami-08b5b3a93ed654d19 \
                            --instance-type t2.micro \
                            --query Instances[0].InstanceId \
                            --output text"
                        bat instance_id

                        echo "Launched instance is: $instance_id"
                        
                        echo "Waiting for the instance to be in running state..."
                        sh "aws ec2 wait instance-status-ok --instance-ids ${instance_id}"
                        echo "Wait completed"

                        echo "Launched and Deployed successfully..."
                        
                           }
                    }
            }
    }
}
