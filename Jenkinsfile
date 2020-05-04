def myVariable = "foo"
def jiraId = ['DSTT-1978','DSTT-2020','DSTT-2121']

pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'File Checkout Script'
		echo "My variable is ${myVariable}"
		 for (ji in jiraId) 
		    {  echo "Jira Id is  ${ji}" }
                
                
            }
        }
        
    }
}
