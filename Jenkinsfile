node {
      try {
          notifyBuild('STARTED')  
  	stage('Code Checkout')
  	{
  		git url: 'https://github.com/daxeos/RTSP-Stream-Video-Capturer.git', branch: 'main', credentialsId: 'shubham_github'
	}   
    	stage('Build Stage')
	{       
        	sh label: '', script: '''  	
	        docker build -t knagu/daxeosopentok:$BUILD_NUMBER -f docker/Dockerfile .
        	docker rmi -f knagu/daxeosopentok:$BUILD_NUMBER
      		'''
	  	echo "Build Successful"
	}             
        stage('Push Image to Hub'){
            sh label: '', script: '''                         
            docker push knagu/daxeosopentok:$BUILD_NUMBER
            docker rmi -f knagu/daxeosopentok:$BUILD_NUMBER
            '''                        
    	}
        stage ('Workspace Cleanup') {
	    cleanWs()                           
	}
      } 
      catch (e) {
      	// If there was an exception thrown, the build failed
      	currentBuild.result = "FAILED"
     	throw e
      } 
      finally {
      	// Success or failure, always send notifications
	notifyBuild(currentBuild.result)
      }
 }

  def notifyBuild(String buildStatus = 'STARTED') {
    // build status of null means successful
    buildStatus =  buildStatus ?: 'SUCCESSFUL'

  // Default values
  def colorName = 'RED'
  def jenkinsURL = 'https://jenkins.daxeos.io/'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${jenkinsURL}/job/${env.JOB_NAME}/${env.BUILD_NUMBER})"

    // Override default values based on build status
    if (buildStatus == 'STARTED') {
      color = 'YELLOW'
      colorCode = '#FFFF00'
    } else if (buildStatus == 'SUCCESSFUL') {
      color = 'GREEN'
      colorCode = '#00FF00'
    } else {
      color = 'RED'
      colorCode = '#FF0000'
    }

    // Send notifications
    slackSend (color: colorCode, message: summary)
  }
