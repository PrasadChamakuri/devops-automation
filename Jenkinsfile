pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']]])
                sh 'mvn clean install'
            }
        }
                stage('Build docker image'){
            steps{
                script{
                    sh 'export DOCKER_BUILDKIT=1'
                    sh 'docker build -t prasadchamakuri/devops-integration .'
                }
            }
        }
                stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u prasadchamakuri -p ${dockerhubpwd}'

}
                   sh 'docker push prasadchamakuri/devops-integration'
                }
            }
        }
        
    }
}
