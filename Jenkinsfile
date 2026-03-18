pipeline{
    agent any

    environment{
        IMAGE_NAME= 'tech365/mymoviepulse'
        IMAGE_TAG= 'v1'
        DOCKER_CREDENTIALS_ID = "dockerlogin"
    }

    stages{
        stage('checkout code'){
            steps{
                git branch: 'main', url:'https://github.com/waleolajumoke/moviepulse.git'
            }
        }

        stage("Build docker image"){
            steps{
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage("Login to docker hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}")])
            }
        }

        stage("push to docker hub"){
            steps{
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }

    post{
        success{
            echo "React image build and pushed successfully"
        }
        failure{
            echo "pipeline failed"
        }
    }
}
