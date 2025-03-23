pipeline {
    agent any

    environment {
        ANSIBLE_HOSTS = "inventory.ini"
        PLAYBOOK = "nginx-playbook.yml"
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
                ansible-playbook -i $ANSIBLE_HOSTS $PLAYBOOK
                '''
            }
        }
    }

    post {
        failure {
            echo "Deployment failed! Rolling back..."
            sh '''
            ansible-playbook -i $ANSIBLE_HOSTS rollback.yml
            '''
        }

        success {
            echo "Deployment succeeded!"
        }
    }
}
