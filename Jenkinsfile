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
                script{
                   sh 'docker login -u anusha1908 -p Anusha1908'
                    sh 'docker push  anusha1908/cicdpipeline'
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
