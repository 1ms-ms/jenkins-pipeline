pipeline{
    agent any
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
        stage("Log in to ECR"){
                sh """
                    aws ecr get-login --no-include-email --region eu-west-1
                """
        }
         stage("Push to ECR"){
            steps   {
                sh """
                    docker tag flask_app 537646401150.dkr.ecr.eu-west-1.amazonaws.com/flask_repo:latest
                """
                sh """
                    docker push 537646401150.dkr.ecr.eu-west-1.amazonaws.com/flask_repo:latest
                """
            }    
        }
    }
}
