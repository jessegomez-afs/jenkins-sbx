pipeline {
  agent any

  environment {
    AWS_DEFAULT_REGION = "us-east-1"
  }

  stages {
    stage('Launch EC2 Instance and Deploy Web App') {
      steps {
        withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'arn:aws:iam::269053967623:user/jerkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          script {
            // Launches an EC2 instance
            sh "aws.exe ec2 run-instances --image-id ami-08b5b3a93ed654d19  --instance-type t2.micro  --query Instances[0].InstanceId  --output text"

            // Wait for the instance to be in running state
            sh "aws ec2 wait instance-status-ok --instance-ids ${instance_id}"

            echo "Wait completed"
          }
        }
      }
    }
  }
}
