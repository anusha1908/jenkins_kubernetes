pipeline {
    agent any
    stages{
       stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], userRemoteConfigs: [[url: 'https://github.com/anusha1908/https-github.com-devopshint-jenkins-kubernetes-example.git']]])
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
                   sh 'docker login -u anusha1908 -p dckr_pat_K10y0IybdJZDgXtoT-ggg90QY2U'
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
