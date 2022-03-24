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
         stage("Push to ECR"){
            steps   {
                sh """
                    docker tag flask_app 537646401150.dkr.ecr.eu-west-1.amazonaws.com/flask_repo:latest
                """
                withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {
                     sh """
                    docker push 537646401150.dkr.ecr.eu-west-1.amazonaws.com/flask_repo:latest
                    """
                }
            }    
        }
    }
}
