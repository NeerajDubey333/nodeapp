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
		    steps{
               withCredentials([string(credentialsId: 'docker hub', variable: 'dockerHubPwd')]) {
		       echo "pass ${dockerHubPwd}"
		       sh "docker login -u dubeyn802 -p ${dockerHubPwd}"
		       sh "docker push dubeyn802/nodeapp:${DOCKER_TAG}"
                }
		    }
	    }
            
        }
}   
                

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}

