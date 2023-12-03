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
                    sh 'docker build -t anusha1908/cicdpipeline .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
               script {
    docker.withRegistry('https://registry-1.docker.io', 'dockerhub') {
        
        docker.image('anusha1908/cicdpipeline').push()
    }
}

            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'Kubeconfpwd')
                }
            }
        }
    }
}
