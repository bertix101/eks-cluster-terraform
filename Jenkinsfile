pipeline {
    agent any

    stages {
        stage('Clone Terraform Repo') {
            steps {
                echo 'Cloning repository ...'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bertix101/eks-cluster-terraform.git']])
            }
        }
        stage('Terraform provision') {
            steps {
                sh """
                    terraform init
                    terraform plan
                    terraform apply --auto-approve
                """
            }
        }
        stage('Licence to kill') {
            steps {
                input message: 'Destroy terraform resources?'
            }
        }
        stage('Search and destroy') {
            steps {
                sh 'terraform destroy --auto-approve'
            }
        }
    }
}
