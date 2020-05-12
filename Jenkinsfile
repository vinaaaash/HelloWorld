#!groovy

def jiraId
def commitId
def values = []
//def pathFinderCommand = []
properties = null     

def loadProperties() {
        properties = new Properties()
        File propertiesFile = new File("${workspace}/JenkinsfileConfig.properties")
        properties.load(propertiesFile.newDataInputStream())
    }
def checkoutGitRepository(comm){
          
	  checkout(
          [$class: 'GitSCM',
   	  branches: [[name: comm]],
          doGenerateSubmoduleConfigurations: false,
          extensions: [[$class: 'CheckoutOption', timeout: 10],[$class: 'RelativeTargetDirectory', relativeTargetDir: properties.PATH]],
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
		  stage ('Sparse Checkout'){
			  steps {
				  script{
					 //loadProperties()
					 jiraId="${properties.JIRA}".split(',')
					  sh "rm -rf ${workspace}/sparse/*"
					
				  for(ji in jiraId)
					  { 
				           echo "Entering for loop with array value ${ji}"
				           def command = "git log --pretty=format:\"%s %H\" | grep ${ji} | awk \'{print \$NF}\'"
					   //echo command
				           
					   commitId = sh(script: command, returnStdout: true)
               				   echo "value of commitId variable: ${commitId}"
					  
				           commitId.split('\n').every
						  {
						   //values.add(it)
						   def srcFiles="git show --pretty=\"\" --name-only ${it}"
					           source = sh(script: srcFiles, returnStdout: true)
						   echo "value of source variable: ${source}"
					           source=source.trim()
						   echo "Printing Source and Destination : ${source} ${workspace}/sparse"
						   sh "cp --parents ${source} ${workspace}/sparse"
							  
					   }
				           
					   
                                          }
					  
					  
			          

				  }
        }
		  }
    /*   stage ('Checkout Specific File'){
            steps {
		    script{
			for(val in values)
       			{
          			echo "Entering checkout stage: for loop: value ${val}"
         			//checkoutGitRepository(val)
				
				//Files.copy(source, target)

       			} // for closing
              		  } //checkout script close
                
            	  } // checkout steps close
                     	} // checkout stage close
	*/
	       } // stages closing
          } // pipeline closing
