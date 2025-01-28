pipeline {
    agent any
    
    environment {
        // Using SSH key stored in Jenkins credentials
        EC2_SSH_KEY = credentials('EC2_SSH')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        AWS_ACCESS_KEY_ID = AKIATBTUX6BEFW2HY24G
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout scm
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

