pipeline{
    agent any 
 
    stages
    {
        stage('Build')
        {
            agent { docker { image 'insect0r/dind:latest' } 
                
            }
            
            steps{
                sh 'rm -rf jenkins-argocd || true '
                sh 'git clone https://github.com/ankit-groverDevops/jenkins-argocd.git'
                sh 'docker build -t insect0r/jenkins-argocd:latest -f jenkins-argocd/Dockerfile jenkins-argocd/'
            
            }
        }
        
        
        stage('PUSH to dockerhub')
        {
            
            steps{
        withCredentials([usernamePassword(credentialsId: 'docker-login', passwordVariable: 'secret', usernameVariable: 'access')]) {
         sh 'docker login -u ${access} -p ${secret}'
        }
     sh 'docker push insect0r/jenkins-argocd:latest '
        
                
                
            }
        }
    
        }
   
        
    }
