pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'File Checkout Script'
                checkout(
		        [$class: 'GitSCM', branches: [[name: '*/master']], 
		        doGenerateSubmoduleConfigurations: false, 
		        extensions: [[$class: 'CheckoutOption', timeout: 1]], 
		        submoduleCfg: [], 
		        userRemoteConfigs: [[url: 'https://github.com/vinaaaash/HelloWorld.git']]])
                
            }
        }
        
    }
}
