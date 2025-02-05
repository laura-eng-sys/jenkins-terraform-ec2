pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = 'us-east-1'
    }
    stages{
        stage('Checkout SCM'){
            steps{
                script{
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/laura-eng-sys/jenkins-terraform.git']])
                }
            }
        }
        stage('Initializing ec2'){
            steps{
                script{
                    dir('ec2/ec2-creation'){
                         sh 'terraform init'
                    }
                }
            }
        }
        stage('validating ec2'){
            steps{
                script{
                    dir('ec2/ec2-creation'){
                         sh 'terraform validate'
                    }
                }
            }
        }
        stage('terraform plan ec2'){
            steps{
                script{
                    dir('ec2/ec2-creation'){
                         sh 'terraform plan'
                    }
                }
            }
        }
         stage('terraform apply ec2'){
            steps{
                script{
                    dir('ec2/ec2-creation'){
                         sh 'terraform apply --auto-approve'
                    }
                }
            }
        }
    }
}    
