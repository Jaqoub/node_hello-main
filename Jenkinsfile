pipeline {
  agent any
  stages {
    stage('Check Docker') {
      steps {
        sh '''
          echo "PATH in Jenkins: $PATH"
          which docker
          docker --version
          docker run hello-world
        '''
      }
    }
  }
}
