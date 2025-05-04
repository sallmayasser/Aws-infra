pipeline {
    agent {
        docker {
            image 'hashicorp/terraform:latest' 
            args '--entrypoint=""'
        }
    }

    environment {
        TF_IN_AUTOMATION = 'true'
    }

    stages {
        stage('Terraform Apply') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-creds-id'
                ]]) {
                    sh '''
                        export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                        export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                        git clone https://github.com/sallmayasser/Aws-infra.git
                        cd Aws-infra

                        terraform init
                        terraform apply --auto-approve 
                    '''
                }
            }
        }
    }
}
