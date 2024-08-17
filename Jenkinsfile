pipeline{
    agent{
        node{
            label 'JenkinsSlaveNodeLabel'
        }
    }
    stages{
        stage('Checkout code stage'){
            steps{
                git url: 'https://github.com/Abhi9-g/cicdprojectrepo.git', branch: 'main'
            }
        }
        stage('Build Docker Image stage'){
            steps{
                sh 'docker build -t myimage .'
            }
        }
        stage('Push image to DockerHub stage'){
            steps{
                sh 'docker tag myimage abhi9d/myimage'
                sh 'docker push abhi9d/myimage'
            }
        }
        stage('Deploy to kubernetes'){
            steps{
                sh 'kubectl apply -f my-deployment.yml'
            }
        }
    }
}