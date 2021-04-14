pipeline {    
    agent {
        kubernetes {
            label 'kubectl'
        }
    }
    stages {
        stage('Source') {
            steps {
                git branch: 'develop', url: 'http://gitlab.gitlab.svc.cluster.local:31080/root/spring-boot-helloworld-deployment.git'
            }
        }
        stage('Deploy') {
            steps {
                container('kubectl') {
                    withKubeConfig([credentialsId: 'k8s-cluster-admin-kubeconfig'
                                    ]) {
                        sh 'kubectl apply -f kubernetes/'
                    }                      
                }
            }
        }
    }
}
