pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Such-a/test.git', branch: 'main'
            }
        }

        stage('Run Script') {
            steps {
                sh 'bash hello.sh'
            }
        }
    }
}
