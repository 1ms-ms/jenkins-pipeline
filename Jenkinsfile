pipeline{
    agent any
    environment {
    AWS_ACCOUNT_ID=”537646401150”
    IMAGE_REPO_NAME=”flask_repo”
    IMAGE_TAG=”latest”
    REPOSITORY_URI = “537646401150.dkr.ecr.eu-west-1.amazonaws.com/flask_repo”
    }
    stages  {
        stage('Initialize'){
            steps {
                script {
                    def dockerHome = tool 'myDocker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                    }
                  }
            }
        stage("build"){
            steps   {
                sh """
                    docker build -t flask_app .
                """
            }    
        }
         stage("Push to ECR"){
            steps   {
                sh """
                    docker tag flask_app $(REPOSITORY_URI):$(IMAGE_TAG)
                """
                sh """
                    docker push $(REPOSITORY_URI):$(IMAGE_TAG)
                """
            }    
        }
    }
}
