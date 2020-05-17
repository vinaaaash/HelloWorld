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
     stage ('Email'){
            steps {
		    script{
			emailIds = sh (script: 'git --no-pager show -s --format=\'%ae\'',returnStdout: true).trim()
            		echo "Git committer email: ${emailIds}"
			    emailext attachLog: true, attachmentsPattern: '.pdf', body: 'Test Body', compressLog: true, mimeType: 'text\\html', recipientProviders: [upstreamDevelopers()], subject: 'Test', to: 'vinaaaash@gmail.com'
              		  } //checkout script close
                /*    script {mail (to: "${properties.emailIds}",
				  subject: "Microservice: '${properties.microServName}' (${env.BUILD_NUMBER}) successfull.",
				  body: "Microservice name: ${properties.microServName}\nGCP deployment: ${properties.GCPdeployment}\nOn-prem deployment:${properties.Onpremdeployment}\n\nPlease visit ${env.BUILD_URL} for further information.");

emailext subject:"Build of ${microServName} SUCCESSFUL!!!",
body:"<table><tr><td>Job Name</td><td>: ${currentBuild.fullDisplayName} </td></tr>"+
"<tr><td>Unit Test report</td><td>: <a href='$BUILD_URL/testReport/'>Click here</a> </td></tr>"+
"For more details please check the logs: $BUILD_URL",
to: emailIds,
mimeType:'text/html'
}*/
            	  } // checkout steps close
                     	} // checkout stage close
	
	       } // stages closing//
          } // pipeline closing// more changes
