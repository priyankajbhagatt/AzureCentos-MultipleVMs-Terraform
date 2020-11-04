pipeline {
    agent {
        node {
            label 'master'
        }
    }

    stages {
  
      stage ('Check Terraform Version') {
         steps {
            script {
            def tfhome = tool name: 'terraform' 
            env.PATH = "${tfhome}:${env.PATH}"
          }
         // sh 'terraform --version'
         }
      
        }
        stage('git clone') {
            steps {
                sh 'whoami'
                //sh 'sudo rm -r *'
               // git url: 'git@github.com:sachinladde/MyWork.git' 
                 git credentialsId: '24120fd5-a5de-40b1-a325-4ddf72e3f8b6', url: 'https://github.com/sachinladde/AzureCentos-MultipleVMs-Terraform.git/' 
                 // below line cloned the repo which will help to auto trigger the webhook
                 //sh 'git clone git@github.com:sachinladde/AzureCentos-MultipleVMs-Terraform.git' 
            }
        }
       
        stage('terraform plan') {
            steps {
                  //  sh 'ls ;  terraform plan -out=plan -input=false -var subscription_id=$AZURE_SUBSCRIPTION_ID -var client_id=$AZURE_CLIENT_ID -var client_secret=$AZURE_CLIENT_SECRET -var tenant_id=$AZURE_TENANT_ID'
                // }
//  Added Azure Cli & Azure cred plugins and added global cred in jenkins. Tried to avoid keeping the .tfvars out of repo but it seems its not possible. Below code gave error as azure cli wont support service principle //
           // withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'AzurePortal',usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
// This is service principle login code. 
                //withCredentials([azureServicePrincipal('Azsrv')]) {
                //sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                //sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
                sh 'terraform --version'
                sh 'terraform init'
                sh 'terraform plan -out=tfplan -input=false'
                

                //}
            }
        }
     stage('terraform apply') {
            steps {
                sh 'echo "Executing the Plan....!!"'
                sh 'terraform apply "tfplan"'
                sh 'echo "Terraform Apply Execution Ended. Please check if resources are created in Azure"'
            }
        }
        
        stage('terraform ended') {
            steps {
                sh 'echo "Terraform Code Ended....!!"'
            }
        }

    
    }
}
