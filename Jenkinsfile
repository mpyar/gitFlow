String checkDiff(String folderName) {
	String diff = bat(script:  ''' 
	                @echo off
	                set diff='''+folderName+'''
	                rem echo %diff%
					if '%diff%'=='Hussain' (echo true) else (echo false)''', returnStdout: true).trim()
	return diff
}

pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                
            script{
                env.diff_Flag = checkDiff('Hussain')
            }
            script {
                echo bat (returnStdout:true, script: 'set diff_Flag')
            }
                
            }
        }
        stage('Test') { 
            when {
                allOf{
                environment name: 'diff_Flag', value: 'true'
                }
            }
            steps {
                bat 'echo TestPassed'
            }
        
        }
    }
}
