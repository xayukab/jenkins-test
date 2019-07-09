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
                git branch: "master", url: 'https://enggbuild@bitbucket.org/appsone/appsone-2.0-installer-scripts.git', credentialsId: "fd197b00-fd06-4632-a018-36134111e086"
            }
        }
        
        stage('Copy Appsone Services'){
          steps {
                        copyArtifacts filter: '**/*.tar.gz', fingerprintArtifacts: true, projectName: 'Appsone-2.0/com.appnomic.appsone$pipeline', selector: specific("${params.PIPELINE_BUILD_NUMBER}")
                        copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'appsone-controlcenter', selector: specific("${params.CONTROL_CENTER_BUILD_NUMBER}")
                        copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'appsone-ui-service', selector: specific("${params.UI_BUILD_NUMBER}")
                }
         }
    }
}
