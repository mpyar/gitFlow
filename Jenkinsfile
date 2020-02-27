#!/usr/bin/env groovy
String checkDiff(String folderName){
    echo folderName
   // String diff=bat label: '', returnStdout: true, script: 'echo "true"'
    String diff=bat(returnStdout: true, script: '''echo "true"''').trim()
    return diff
    
}

pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                
                withAnt(installation: 'Ant')
                {
                    bat 'ant -version'
                }
            
            checkout poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/mpyar/gitFlow.git']]]
            
            script{
                //env.diff_Flag = checkDiff('Hussain')
                env.diff_Flag = bat(returnStdout: true, script: 'echo "true"').trim()
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
