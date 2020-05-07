#!groovy

def jiraId
def shelloutput
def values = []

properties = null     

def loadProperties() {
        properties = new Properties()
        File propertiesFile = new File("${workspace}/JenkinsfileConfig.properties")
        properties.load(propertiesFile.newDataInputStream())
    }
def checkoutGitRepository(comm, poll = true, timeout = 10, depth = 0){
          
	  checkout(
          [$class: 'GitSCM',
   	  branches: [[name: comm]],
          doGenerateSubmoduleConfigurations: false,
          extensions: [[$class: 'CheckoutOption', timeout: 10],[$class: 'RelativeTargetDirectory', relativeTargetDir: '/var/lib/jenkins/workspace/multibranch-pipeline-test_master/chkoutdir']],
          submoduleCfg: [],
          userRemoteConfigs: [[credentialsId: properties.PASSWORD, url: properties.URL]]])
              }

pipeline {
    agent any
	stages {
		stage ('Load Properties'){
			steps{
			loadProperties()
			}
		}
		  stage ('Fetch Commit Ids'){
			  steps {
				  script{
					 //loadProperties()
					 jiraId="${properties.JIRA}".split(',')
					
				  for(ji in jiraId)
					  { 
				           echo "Entering for loop with array value ${ji}"
				           def command = "git log --pretty=format:\"%s %H\" | grep ${ji} | awk \'{print \$NF}\'"
					   //echo command
					   shelloutput = sh(script: command, returnStdout: true)
               				   echo "val of ret ${shelloutput}"
				           shelloutput.split('\n').every{values.add(it)}
						  
					   
                                          }	 
			          

				  }
        }
		  }
        stage ('Checkout Specific File'){
            steps {
		    script{
			for(val in values)
       			{
          			echo "Entering checkout stage: for loop: value ${val}"
         			checkoutGitRepository(val, poll = true, timeout = 10, depth = 0)

       			} // for closing
              		  } //checkout script close
                
            	  } // checkout steps close
                     	} // checkout stage close
	
	       } // stages closing
          } // pipeline closing
