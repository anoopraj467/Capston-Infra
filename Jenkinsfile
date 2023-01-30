pipeline {
    agent any

    stages {
        stage('Poll SCM') {
            steps {
              git credentialsId: 'git-token', url: 'git@github.com:anoopraj467/Capston-Infra.git'
            }
        }
        stage('Terraform Format'){
            steps{
                sh 'terraform fmt'
            }
        }
        stage('Terraform init'){
            steps{
                sh 'terraform init'
            }
        }
        stage('Terraform validate'){
            steps{
                sh 'terraform validate'
            }
        }
        stage('Terraform plan'){
            steps{
                sh 'terraform plan -out myplan'
            }
        }
        stage('Approval') {
        steps {
            script {
          def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
        }
      }
    }
        stage('Terraform apply'){
           steps {
                sh 'terraform apply -input=false myplan'
         }
        }
    }
}
