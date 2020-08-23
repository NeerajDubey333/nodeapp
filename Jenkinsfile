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
		stage('Dockerhub push'){
			withCredentials([string(credentialsId: 'docker hub', variable: 'dockerHubPwd')]) {
				sh "dockerlogin -u  NeerajDubey333 -p ${dockerHubPwd}"
                   }
			
		}
            }
        }
}   
                

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}

