pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"   
        registry = "uday1011/cicd-e2e"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                git branch: 'main', 
                credentialsId: 'github-credential', 
                url: 'https://github.com/Uday599/cicd-end-to-end-abhishek.git'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    //sh '''
                    //echo 'Buid Docker Image'
                    // docker build -t uday1011/cicd-e2e:${BUILD_NUMBER} .
                    //'''
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()

                    //sh '''
                    // echo 'Push to Repo'
                    // docker push uday1011/cicd-e2e:${BUILD_NUMBER}
                    // '''
                        }
                    }       
                }    
  
            }
        }
}
