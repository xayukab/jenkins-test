pipeline {
    agent { label 'First_Slave' }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
    }
    parameters {
        string defaultValue: '', description: '', name: 'PIPELINE_BUILD_NUMBER', trim: true
        string defaultValue: '', description: '', name: 'UI_BUILD_NUMBER', trim: true
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
                    copyArtifacts filter: '**/*.tar.gz', fingerprintArtifacts: true, projectName: 'Appsone-2.0/com.appnomic.appsone$pipeline', selector: specific("${params.PIPELINE_BUILD_NUMBER}")
                    copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'appsone-ui-service', selector: specific("${params.UI_BUILD_NUMBER}")
                }
         }
    }
}
