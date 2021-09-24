node {
  	stage('Code Checkout')
  	{
  		git url: 'https://github.com/knagu/RTSP-Stream.git', branch: 'main'
	}   
    	stage('Build Stage')
	{       
        	sh label: '', script: '''  	
	        docker build -t knagu/daxeosopentok:$BUILD_NUMBER -f docker/Dockerfile .
      		'''
	  	echo "Build Successful"
	}             
        stage('Push Image to Hub'){
         withCredentials( [usernamePassword( credentialsId: 'nagendra_dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
            sh label: '', script: '''                          
            docker login --username $USERNAME --password $PASSWORD
            docker push knagu/daxeosopentok:$BUILD_NUMBER
            docker rmi -f knagu/daxeosopentok:$BUILD_NUMBER
            '''                        
    	}
       }
        stage ('Workspace Cleanup') {
	    cleanWs()                          
       }
} 
