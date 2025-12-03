// Jenkinsfile (Simple Deployment on Jenkins Host)

pipeline {
    agent any
    
    // Environment: Define key variables
    environment {
        // Your Docker Hub image name
        IMAGE_NAME = "rijin1906/amazon" 
        
        // Name for the container
        CONTAINER_NAME = 'amazon-clone-web' 
        
        // Map host port 8080 to container port 80
        PORT_MAPPING = '8080:80' 
    }

    stages {
        
        // Stage 1: Checkout Code
        stage('Checkout Code') {
            steps {
                echo 'Fetching source code (Jenkinsfile).'
                checkout scm
            }
        }
        
        // Stage 2: Pull the Image from Docker Hub
        stage('Pull Image') {
            steps {
                echo "Pulling image ${IMAGE_NAME} from Docker Hub..."
                // Use 'sh' to run the standard Docker pull command
                sh "/usr/local/bin/docker pull ${IMAGE_NAME}:latest" 
                echo 'Image pulled successfully.'
            }
        }
        
        // Stage 3: Deploy/Run the Container
        stage('Run Application') {
            steps {
                echo 'Stopping and removing old container (if exists)...'
                // Stop and remove old container to ensure the new one can start
                sh "/usr/local/bin/docker stop ${CONTAINER_NAME} || true && /usr/local/bin/docker rm ${CONTAINER_NAME} || true"
                
                echo 'Running new container...'
                // Run the new container using the defined variables
                sh "/usr/local/bin/docker run -d --name ${CONTAINER_NAME} -p ${PORT_MAPPING} ${IMAGE_NAME}:latest"
                
                echo "Application is running on the Jenkins host machine at port 8080."
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline Succeeded! Check the Jenkins dashboard for the flow visualization.'
        }
    }
}
