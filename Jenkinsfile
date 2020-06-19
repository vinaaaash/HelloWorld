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
def checkoutGitRepository(){
          
	  checkout(
          [$class: 'GitSCM',
   	  branches: [[name: '*/master']],
          doGenerateSubmoduleConfigurations: false,
	   extensions: [[$class: 'CheckoutOption', timeout: 10]],
          submoduleCfg: [],
          userRemoteConfigs: [[credentialsId: properties.PASSWORD, url: properties.URL]]])
              }

pipeline {
    agent any
	stages {
		stage ('Load Properties'){
			steps{
			loadProperties()
			cleanWs()
			checkoutGitRepository()
			dir("${workspace}@tmp") {
                        deleteDir()
                        }
			}
		}
		  stage ('Sparse Checkout'){
			  steps {
				  script{
					 sh 'mkdir sparsechkout'
					 jiraId="${properties.JIRA}".split(',')
					  //sh "rm -rf ${workspace}/sparse/*"
					
				  for(ji in jiraId)
					  { 
				           echo "Entering for loop with array value ${ji}"
				           def command = "git log --pretty=format:\"%s %H\" | grep ${ji} | awk \'{print \$NF}\'"
					   //echo command
				           
					   commitId = sh(script: command, returnStdout: true)
               				   echo "value of commitId variable: ${commitId}"
					  
						  commitId.split('\n').every{values.add(it)}
					  }  //for jiraId closed
						  for (val in values)
						  {
						   //def srcFiles="git show --pretty= --name-only ${val}"
			def srcFiles="git diff-tree --no-commit-id --name-only -r ${val} | xargs tar -rf mytarfile.tar | xargs tar -xvf mytarfile.tar -C sparsechkout"
					           source = sh(script: srcFiles, returnStdout: true)
						   source=source.trim()
						   echo "value of source variable: ${source}"
					           
						   echo "Printing Source and Destination : ${source} ${workspace}/sparsechkout"
						   //sh "cp --parents ${source} ${workspace}/copydir"
					           //sh 'rm mytarfile.tar'
							  
					   } // for values closed
				           } // scripts closed
					  
        } //step closed
		  } // stage closed


stage('Demo') {
    echo 'Hello world'
    sayHello 'Avi'
}
	
	       } // stages closing//
          } // pipeline closing// more changes
