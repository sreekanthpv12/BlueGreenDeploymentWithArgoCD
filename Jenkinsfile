pipeline {
    agent any
    environment {
        build_number = "${env.BUILD_ID}"
        KUBECONFIG = '/var/jenkins_home/.kube/config'
    }
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/sreekanthpv12/BlueGreenDeploymentWithArgoCD.git'
            }
        }
        
        stage('Package Helm Chart') {
            steps {
                sh "helm package ."
            }
        }
        
        stage('Delete Old Helm Release') {
            steps {
                sh "helm delete bluegreen || true"
            }
        }
        
        stage('Install Helm Chart') {
            steps {
                sh "helm install bluegreen ./blue-green-0.1.0.tgz"
            }
        }
    }
}

