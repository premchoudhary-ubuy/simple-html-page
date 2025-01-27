pipeline {
    agent any
    
    environment {
        // Using SSH key stored in Jenkins credentials
        EC2_SSH_KEY = credentials('jenkins-ssh-key')
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
                    ansible-playbook ./ansible/playbooks/nginx-setup.yml  --user ubuntu --private-key $EC2_SSH_KEY
                    '''
                }
            }
        }
    }
}

