pipeline {
    agent any
    environment {
        RESPONSE_1 = '"Hello from Container 1"'
        RESPONSE_2 = '"Hello from Container 2"'
        RESPONSE_3 = '"Hello from Container 3"'
        PORT_1 = '"3000"'
        PORT_2 = '"3001"'
        PORT_3 = '"3002"'
    }
    stages {
        stage('Build Docker Images') {
            steps {
                script {
 sh """
                       docker run hello-world 
                    """                    
                    echo "docker build --build-arg RESPONSE_MESSAGE=${RESPONSE_2} --build-arg PORT=${PORT_2} -t container2:latest ."
                    echo "docker build --build-arg RESPONSE_MESSAGE=${RESPONSE_3} --build-arg PORT=${PORT_3} -t container3:latest ."
                }
            }
        }
        stage('Run Containers') {
            steps {
                script {
                    echo "docker run -d -p 3000:3000 container1:latest"
                    echo "docker run -d -p 3001:3001 container2:latest"
                    echo "docker run -d -p 3002:3002 container3:latest"
                }
            }
        }
        stage('Verify Containers') {
            steps {
                script {
                    echo "sleep 10"
                    echo "curl http://localhost:3000"
                    echo "curl http://localhost:3001"
                    echo "curl http://localhost:3002"
                }
            }
        }
    } 
}
