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
					 emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
				 }  
				 failure {  
					 emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
				 }  
			}
				
         }
    }
}
