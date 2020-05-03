pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'File Checkout Script'
                sh 'git log --pretty=format:"%s %H" |grep DSTT-2121 | awk '{print $NF}''
                
            }
        }
        
    }
}
