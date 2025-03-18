pipeline {
    agent any
    environment {
        TERRAFORM_HOME = 'C:\\Users\\jgome\\bin'
        PROJECT_HOME = 'C:\\Users\\jgome\\jenkins-sbx' 

    stages {
        stage('Terraform Init') {
            steps {
                script {
                    def tfInit = "cd ${PROJECT_HOME} && ${TERRAFORM_HOME}\\terraform init"
                    bat tfInit
                }
            }
        }
        stage('Terraform Plan') {
            steps {
                script {
                    def tfPlan = "cd ${PROJECT_HOME} && ${TERRAFORM_HOME}\\terraform plan"
                    bat tfPlan
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                script {
                    def tfApply = "cd ${PROJECT_HOME} && ${TERRAFORM_HOME}\\terraform apply -auto-approve"
                    bat tfApply
                }
            }
        }
    }
}
