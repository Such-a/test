pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/your-username/jenkins-test.git', branch: 'main'
            }
        }

        stage('Run Script') {
            steps {
                sh 'bash hello.sh'
            }
        }
    }
}
