#!groovy

def jiraId = ['DSTT-1978','DSTT-2020','DSTT-2121']
def commitIdList = []
def workingDir = new File("F:\\JavaProj")

pipeline {
    agent any
	stages {
		  stage ('forloop'){
			  steps {
				  script{
					  Process proc = "git log --pretty=format:\"%s %H\"".execute(null,workingDir)
					  def var1=proc.text
					  
				  for(ji in jiraId)
					  { 
				           echo "Entering for loop with value ${ji}"
					   //bat 'wmic computersystem get name'
					   //echo bat(returnStdout: true, script: 'set')
				           var1.eachLine{
                                           if (it.startsWith($ji))
                                           commitIdList.add(it.split(' ')[1])
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
