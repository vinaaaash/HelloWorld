pipeline {
    agent any
	stages {
		
		  stage ('forloop'){
            steps {
		    def jiraId = ['DSTT-1978','DSTT-2020','DSTT-2121']
		    def commitIdList = []
                echo "Entering for loop"
            }
        }	
		
		
        stage ('git'){
            steps {
                checkout(
		        [$class: 'GitSCM', 
			branches: [[name: '*/master']], 
		        doGenerateSubmoduleConfigurations: false, 
		        extensions: [[$class: 'CheckoutOption', timeout: 1]], 
		        submoduleCfg: [], 
		        userRemoteConfigs: [[url: 'https://github.com/vinaaaash/HelloWorld.git']]])
            	  }
                     }
	
	       }
          }
