#!groovy
pipeline {
    environment {     
           registryCredentials = credentials('Docker_credential')
    }
    agent { label 'docker' }
    stages{
        stage('git-checkout') {
            steps {
                git branch: 'master', url:'https://github.com/Nithishkumar0064/kubernetes-assignment.git'
            }
        }
        stage('Build docker image'){
            steps {
		        sh 'docker build -t ${registryCredentials_USR}/tomcat4:${BUILD_ID} .'
            }
        }
        stage('Push image to Hub'){
            steps {
                sh 'docker login -u ${registryCredentials_USR} -p ${registryCredentials_PSW}'
		        sh 'docker push ${registryCredentials_USR}/tomcat4:${BUILD_ID}'
            }
        }
        stage('Deploy to kubernetes') {
            steps {
                sh 'kubectl apply -f newpod.yml'
            }
            
        }
        
   }
}
