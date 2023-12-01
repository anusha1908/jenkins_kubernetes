pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/YashodaRG/jenkins_kubernetes']]])
                sh 'cd /var/lib/jenkins/workspace/jenkins_k8s_integration'
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t yashodarg/cicdpipeline .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   sh 'docker login -u yashodarg -p Dockerhub2023$'
                    sh 'docker push  yashodarg/cicdpipeline'
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
