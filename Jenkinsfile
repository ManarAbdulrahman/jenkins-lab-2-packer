pipeline {

    agent {
            kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: packer
    image: hashicorp/packer 
    command: 
    - bash
    tty: true
"""
    }
    }
     environment {
        CREDS = credentials('manar-aws')
        OWNER = "manar"
        PROJECT_NAME = 'k8s-jenkins'
        AWS_ACCESS_KEY_ID= "${CREDS_USR}"
        AWS_SECRET_ACCESS_KEY= "${CREDS_PSW}"
    }
    stages {
       
     stage ('build') {
         
            steps {
                sh "make init"
                
                sh "packer build packer.json "
                
            }
        }
    }
     post {
            success {
                build job: "Manar-webserver", wait: false
            //add a commment
            }
        }
        
    }
