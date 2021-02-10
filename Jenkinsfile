pipeline {
    agent any
    environment {
        TFPROJECTFOLDER = 'terraform-demo'
        TFPROJECTREPO = 'https://github.com/peferso/terraform-demo.git'
    }
    stages {
        stage('Clone templates') {
            steps {
                sh '''#!/bin/bash
                mkdir -p ${TF_WORKSPACE_PATH}
                cd ${TF_WORKSPACE_PATH}
                exists=$(ls ${TFPROJECTFOLDER} 2>/dev/null)
                if [ -z $exists ] 
                then
                  git clone ${TFPROJECTREPO}
                else
                  cd ${TF_WORKSPACE_PATH}/${TFPROJECTFOLDER}
                  git checkout main
                  git fetch --all
                  git reset --hard origin/main
                fi
                '''
            }
        }        
        stage('Terraform init') {
            steps {
                sh '''#!/bin/bash
                cd ${TF_WORKSPACE_PATH}/${TFPROJECTFOLDER};
                terraform init;
                '''
            }
        }
        
        stage('Terraform apply') {
            steps {
                sh '''#!/bin/bash
                cd ${TF_WORKSPACE_PATH}/${TFPROJECTFOLDER};
                terraform apply -auto-approve 
                '''
            }
        }
        
        stage('Terraform refresh') {
            steps {
                sh '''#!/bin/bash
                cd ${TF_WORKSPACE_PATH}/${TFPROJECTFOLDER};
                terraform refresh
                '''
            }
        }        
    }
}
