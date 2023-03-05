pipeline{
    agent any
    triggers{
        cron("10 * * * *")
    }
    stages{
        stage("Build Docker Images"){
            steps{
                sh 'docker-compose -f docker-compose-build.yaml build --parallel'
            }
        }

        stage("Tag Docker Images"){
            steps{
                sh "docker tag udagram-api-user '$DOCKER_USERNAME/udagram-api-user:latest'"
                sh "docker tag udagram-api-feed '$DOCKER_USERNAME/udagram-api-feed:latest'"
                sh "docker tag udagram-frontend '$DOCKER_USERNAME/udagram-frontend:latest'"
                sh "docker tag reverseproxy '$DOCKER_USERNAME/reverseproxy:latest'"
            }
        }
        
        stage("Publish Docker Images to DockerHub"){
            steps{
                sh "echo '$DOCKER_PASSWORD' | docker login -u '$DOCKER_USERNAME' -password-stdin"
                sh "docker push '$DOCKER_USERNAME/udagram-api-user:latest'"
                sh "docker push '$DOCKER_USERNAME/udagram-api-feed:latest'"
                sh "docker push '$DOCKER_USERNAME/udagram-frontend:latest'"
                sh "docker push '$DOCKER_USERNAME/reverseproxy:latest'"
            }
        }
    }
}