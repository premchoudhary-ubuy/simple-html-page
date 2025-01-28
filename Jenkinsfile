pipeline {
    agent any
    
    environment {
        // Using SSH key stored in Jenkins credentials
        EC2_SSH_KEY = credentials('EC2_SSH')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        AWS_ACCESS_KEY_ID = credentials('both')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Install boto3 and botocore dependencies on the Jenkins machine
                    sh '''
                    sudo apt-get update
                    sudo apt-get install pip
                    pip install boto3 botocore
                    '''
                }
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Running Ansible Playbook to configure the server
                    sh '''
                    ansible-playbook ./ansible/playbooks/nginx-setup.yml --inventory ./ansible/inventory  --user ubuntu --private-key $EC2_SSH_KEY
                    '''
                }
            }
        }
    }
}

