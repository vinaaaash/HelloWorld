#!groovy

def jiraId = ['DSTT-2121']
//def commitIdList = []
def ret
def values

def checkoutGitRepository(comm, poll = true, timeout = 10, depth = 0){
                checkout(
          [$class: 'GitSCM',
   branches: [[name: comm]],
          doGenerateSubmoduleConfigurations: false,
          extensions: [[$class: 'CheckoutOption', timeout: 10]],[[$class: 'RelativeTargetDirectory', relativeTargetDir: '/var/lib/jenkins/workspace/multibranch-pipeline-test_master/chkoutdit']],
          submoduleCfg: [],
          userRemoteConfigs: [[credentialsId: 'cb6b162a-4202-436c-ab60-44e8886a4de4', url: 'https://github.com/vinaaaash/HelloWorld.git']]])
              }

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
					   values = ret.split('\n') 
                                          }	 
			          
					  echo "Value0 ${values[0]}"
        				  echo "Value1 ${values[1]}"
                                          echo "Value2 ${values[2]}"
				  }
        }
		  }
        stage ('checkout'){
            steps {
		    script{
			for(val in values)
       			{
          			echo "Entering for loop with value ${val}"
         			checkoutGitRepository(val, poll = true, timeout = 10, depth = 0)

       			} // for closing
              		  } //checkout script close
                
            	  } // checkout steps close
                     	} // checkout stage close
	
	       } // stages closing
          } // pipeline closing
