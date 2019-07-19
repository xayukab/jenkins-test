pipeline {
    agent { label 'First_Slave' }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: "master", url: 'https://github.com/abh1sh3k/jenkins-test.git', credentialsId: ""
            }
        }
        
        stage('Copy Appsone Services'){
          steps {
              load "${WORKSPACE}/modulelist"
              echo "${env.PIPELINE_BUILD_NUMBER}"
				copyArtifacts filter: '**/*.tar.gz', fingerprintArtifacts: true, projectName: 'Appsone-2.0/com.appnomic.appsone$pipeline', selector: specific("${env.PIPELINE_BUILD_NUMBER}")
				copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'appsone-ui-service', selector: specific("${env.UI_BUILD_NUMBER}")
            }
			
			post {
				always {  
				 echo 'This will always run'  
				 }  
				 success {  
					 mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "abhishek.d@appnomic.com";  
				 }  
				 failure {  
					 mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "abhishek.d@appnomic.com";  
				 }  
			}
				
         }
    }
}
