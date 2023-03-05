pipeline{
    agent any
    stages{
        stage("Build Docker Images"){
            steps{
                docker-compose -f docker-compose-build.yaml build --parallel                
            }
        }

        stage("Tag Docker Images"){
            steps{
                docker tag udagram-api-user "$DOCKER_USERNAME/udagram-api-user:latest"
                docker tag udagram-api-feed "$DOCKER_USERNAME/udagram-api-feed:latest"
                docker tag udagram-frontend "$DOCKER_USERNAME/udagram-frontend:latest"
                docker tag reverseproxy "$DOCKER_USERNAME/reverseproxy:latest"
            }
        }
        
        stage("Publish Docker Images to DockerHub"){
            steps{
                echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" -password-stdin
                docker push "$DOCKER_USERNAME/udagram-api-user:latest"
                docker push "$DOCKER_USERNAME/udagram-api-feed:latest"                 
                docker push "$DOCKER_USERNAME/udagram-frontend:latest"
                docker push "$DOCKER_USERNAME/reverseproxy:latest"
            }
        }
    }
}