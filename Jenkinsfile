pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
		    sh "docker build . -t dubeyn802/nodeapp:${DOCKER_TAG}"
	    }
		}//stage 1 ennd
	    			
	    stage('Push Docker Image'){
               withCredentials([string(credentialsId: 'docker hub', variable: 'dockerHubPwd')]) {
		       sh "docker login -u NeerajDubey333 -p ${dockerHubPwd}"
		       sh "docker push NeerajDubey333/nodeapp${DOCKER_TAG}"
                }
	    
	    }
            
        }
}   
                

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}

