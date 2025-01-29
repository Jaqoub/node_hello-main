pipeline {
    agent any
    environment {
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }
    stages {
        stage('Docker test') {
            steps {
                sh 'docker run hello-world'
            }
        }
    }
}