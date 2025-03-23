pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://your-git-repo-url.git'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                ansible-playbook -i inventory.ini nginx-playbook.yml
                '''
            }
        }
    }
}

