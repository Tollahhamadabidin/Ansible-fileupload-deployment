pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        ANSIBLE_FORCE_COLOR = 'true'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Tollahhamadabidin/Ansible-fileupload-deployment.git'
            }
        }

        stage('Verify Ansible & Inventory') {
            steps {
                sh '''
                    ansible --version
                    ansible-playbook -i inventory.ini playbook/fileupload-main.yaml --syntax-check
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                    ansible-playbook -i inventory.ini playbook/fileupload-main.yaml
                '''
            }
        }
    }

    post {
        success {
            echo 'Spring Fileupload Service built, pushed, and deployed to stag-server successfully!'
        }
        failure {
            echo 'Ansible deployment pipeline failed. Check console output.'
        }
    }
}
