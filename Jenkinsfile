pipeline {
    agent any
    stages{
      stage('Build Maven') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/anusha1908/jenkins_kubernetes.git']]])
               
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t anusri1908/ci-cd .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
               script {
    docker.withRegistry('https://registry-1.docker.io', 'dockerhub') {
        
        docker.image('anusri1908/ci-cd').push()
    }
}

            }
        }
        stage('Deploying to Kubernetes') {
              steps{
					script {
						kubernetesDeploy(configs: "deploymentservice.yaml" , kubeconfigId: "kubernetes")
						   }
    
                    }
					
					
                    
                }
    }
}
