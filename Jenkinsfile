def build(){
stage('Build'){
checkout(
		        [$class: 'GitSCM', branches: [[name: '*/master']], 
		        doGenerateSubmoduleConfigurations: false, 
		        extensions: [[$class: 'CheckoutOption', timeout: 1]], 
		        submoduleCfg: [], 
		        userRemoteConfigs: [[url: 'https://github.com/vinaaaash/HelloWorld.git']]])
				}
			}
			
/*************** Pipeline Starts ***********************************************/
pipeline {
    agent any
stages {  
stage ('checkout') {
steps {
build()
}
}
}
}
