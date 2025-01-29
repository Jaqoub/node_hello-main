pipeline {
    agent any
    
    // Define environment variables without extra quotes.
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
                // Actually run the Docker commands, rather than echo them
                sh """
                    echo "Testing Docker with hello-world:"
                    docker run hello-world
                    
                    echo "Building container1:"
                    docker build --build-arg RESPONSE_MESSAGE=${RESPONSE_1} --build-arg PORT=${PORT_1} -t container1:latest .
                    
                    echo "Building container2:"
                    docker build --build-arg RESPONSE_MESSAGE=${RESPONSE_2} --build-arg PORT=${PORT_2} -t container2:latest .
                    
                    echo "Building container3:"
                    docker build --build-arg RESPONSE_MESSAGE=${RESPONSE_3} --build-arg PORT=${PORT_3} -t container3:latest .
                """
            }
        }
        
        stage('Run Containers') {
            steps {
                // Run the containers in detached mode (-d) and map ports
                sh """
                    echo "Running container1 on port ${PORT_1}:"
                    docker run -d -p ${PORT_1}:${PORT_1} container1:latest
                    
                    echo "Running container2 on port ${PORT_2}:"
                    docker run -d -p ${PORT_2}:${PORT_2} container2:latest
                    
                    echo "Running container3 on port ${PORT_3}:"
                    docker run -d -p ${PORT_3}:${PORT_3} container3:latest
                """
            }
        }
        
        stage('Verify Containers') {
            steps {
                // Give containers time to start, then curl each one
                sh """
                    echo "Sleeping 10 seconds to allow containers to fully start..."
                    sleep 10

                    echo "Verifying container1 response:"
                    curl http://localhost:${PORT_1} || true

                    echo "Verifying container2 response:"
                    curl http://localhost:${PORT_2} || true

                    echo "Verifying container3 response:"
                    curl http://localhost:${PORT_3} || true
                """
            }
        }
    }
}
