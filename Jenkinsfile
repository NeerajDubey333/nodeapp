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
               withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerHubPwd')]) {
		       echo "pass ${dockerHubPwd}"
		       sh "docker login -u dubeyn802 -p ${dockerHubPwd}"
		       sh "docker push dubeyn802/nodeapp:${DOCKER_TAG}"
                }
		    }
	    }
	    stage ('deploy to k8s'){ 
		    steps{  
			    sh "chmod +x changeTag.sh"
			    sh "./changeTag.sh ${DOCKER_TAG}"
			   sh "scp -o stricthostkeychecking=no services.yml node-app-pod.yml ec2-user@3.89.65.153:/home/ec2-user"
			    script{
				    try{
					    sh "ssh ec2-user@3.89.65.153 kubectl apply -f."
				    }catch(error){
					    sh "ssh ec2-user@3.89.65.153 kubectl create -f."
				    
				    }
			    } 
		    }
	    
	    }
            
        }
}   
                

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}

