pipeline{
    agent any
    stages{
        stage('Checkout code stage'){
            steps{
                git url: 'https://github.com/Abhi9-g/cicdprojectrepo.git', branch: 'main'
            }
        }
        /*stage('Cleanup stage'){
            steps{
                sh 'docker rm -f $(docker ps -aq)'
                sh 'docker rmi -f myimage'
            }
        }*/
        stage('Build Docker Image stage'){
            steps{
                sh 'docker build -t myimage:latest .'
            }
        }
        stage('Push image to DockerHub stage'){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerhub-credentials',
                usernameVariable:'DOCKER_USERNAME',passwordVariable:'DOCKER_PASSWORD')])
                {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag myimage:latest $DOCKER_USERNAME/myimage:latest'
                    sh 'docker push $DOCKER_USERNAME/myimage:latest'
                }
            }
        }
        stage("Kubernetes deployment stage"){
            steps{
                sh 'kubectl apply -f my-deployment.yml'
            }
        }
    }
}