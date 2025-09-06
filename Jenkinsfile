node {
// Define environment variables
env.DOCKERHUB_USERNAME = 'gscomp308'
env.DOCKER_IMAGE_NAME = "gscomp308"
env.DOCKER_IMAGE_TAG = "latest"

// Stage 1: Pull the Git repository.
stage('Git Checkout') {
    echo 'Checking out the Git repository...'
    git url: 'https://github.com/tettolizer/NCC_2025_GSCOMP308.git'
}

// Stage 2: Build the Docker image.
stage('Build Docker Image') {
    echo 'Building the Docker image...'
    sh "docker build -t ${env.DOCKERHUB_USERNAME}/${env.DOCKER_IMAGE_NAME}:${env.DOCKER_IMAGE_TAG} ."
}

// Stage 3: Push the Docker image to Docker Hub.
stage('Push to Docker Hub') {
    echo 'Pushing the Docker image to Docker Hub...'
    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
        sh "docker login -u ${env.DOCKERHUB_USERNAME} -p ${env.DOCKERHUB_PASSWORD}"
        sh "docker push ${env.DOCKERHUB_USERNAME}/${env.DOCKER_IMAGE_NAME}:${env.DOCKER_IMAGE_TAG}"
    }
}

}
