pipeline {
    agent any

    environment {
        REMOTE_HOST = "your_server_ip"
        REMOTE_USER = "your_user"
        SSH_KEY = "~/.ssh/id_rsa"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://your-git-repo-url.git'
            }
        }

        stage('Install Ansible') {
            steps {
                sh '''
                sudo apt update -y
                sudo apt install -y ansible
                '''
            }
        }

        stage('Deploy Nginx with Ansible') {
            steps {
                sh '''
                ansible-playbook -u $REMOTE_USER -i $REMOTE_HOST, --private-key=$SSH_KEY nginx-playbook.yml
                '''
            }
        }
    }

    post {
        failure {
            echo "Deployment failed! Rolling back..."
            sh '''
            ansible-playbook -u $REMOTE_USER -i $REMOTE_HOST, --private-key=$SSH_KEY rollback.yml
            '''
        }

        success {
            echo "Deployment succeeded!"
        }
    }
}
