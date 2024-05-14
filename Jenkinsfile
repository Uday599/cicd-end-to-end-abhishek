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
            stage('Checkout K8S manifest SCM'){
            steps {
                git branch: 'main', 
                credentialsId: 'github-credential', 
                url: 'https://github.com/Uday599/cicd-end-to-end-manifest-files.git'
                    }
                }
                
             stage('Update K8S manifest & push to Repo'){
            steps {
                script{
                    withCredentials([usernamePassword(credentialsId: 'github-credential', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh '''
                        cat deploy.yaml
                        sed -i 19"s/1/${BUILD_NUMBER}/g" deploy.yaml
                        cat deploy.yaml
                        git add deploy.yaml
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push https://github.com/Uday599/cicd-end-to-end-manifest-files.git HEAD:main
                        '''                        
                    }
                }
            }
        }
       // stage('Cleaning up') {
           // steps{
                  //  sh "docker rmi $registry:$BUILD_NUMBER"
                  //  }
}
}
