#!groovy

def jiraId = ['DSTT-2121']
def commitIdList = []
//def workingDir = new File("F:\\JavaProj")
def ret

pipeline {
    agent any
	stages {
		  stage ('forloop'){
			  steps {
				  script{				  
				  for(ji in jiraId)
					  { 
				           echo "Entering for loop value ${ji}"
               				   ret = sh(script: 'git log --pretty=format:\"%s %H\" | grep DSTT-2121', returnStdout: true)
               				   echo "val of ret ${ret}"
					   ret.each{
			                   if (it.startsWith('DSTT-2121'))
                                           echo it.split(' ')
                                           }
				           
					  }
			          
				  }
        }
		  }
        stage ('checkout'){
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
