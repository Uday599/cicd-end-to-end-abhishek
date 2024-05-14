pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
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
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t uday1011/cicd-e2e:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push uday1011/cicd-e2e:${BUILD_NUMBER}
                    '''
                }
            }
        }    
  
    }
}
