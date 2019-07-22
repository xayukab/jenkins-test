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
     
		stage('Verifying build number on Jenkins') {
			steps {
				sh '''
						cat modulelist | grep 'BUILD_NUMBER' | while read line
						do
							build_number=`echo $line | awk -F"=" '{print $2}' | tr -d " "`
							appname=`echo $line | awk -F"=" '{print $1}' | awk -F"." '{print $2}'|tr -d " "`
							if [ appname="PIPELINE_BUILD_NUMBER"] || [ appname="GRPC_BUILD_NUMBER" ] || [ appname="TRANSACTIONBROKER_BUILD_NUMBER" ] || [ appname="COMPONENT_AGENT_BUILD_NUMBER" ];then
								curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/Appsone-2.0/${build_number}/ | grep -q "ERROR 404"
								if [ $? -eq 0 ];then
									appsonebuildresult=0
								fi  
							elif [ appname="UI_BUILD_NUMBER" ];then
								curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/appsone-ui-service/${build_number} | grep -q "ERROR 404"
								if [ $? -eq 0 ];then
									uibuildresult=0
								fi
							elif [ appname="LOGFORWARDER_BUILD_NUMBER" ];then
								curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/log-forwarder/${build_number} | grep -q "ERROR 404"
								if [ $? -eq 0 ];then
									logforwarderbuildresult=0
								fi
							elif [ appname="CONTROL_CENTER_BUILD_NUMBER" ];then
								curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/appsone-controlcenter/${build_number} | grep -q "ERROR 404"
								if [ $? -eq 0 ];then
									controlcenterbuildresult=0
								fi
							elif [ appname="JIM_BUILD_NUMBER" ];then
								curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/Java-Intrusive-Agent/${build_number} | grep -q "ERROR 404"
								if [ $? -eq 0 ];then
									jimbuildresult=0
								fi
							fi  
						done
				'''
				script {
					if(env.appsonebuildresult==0){
						emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
											Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
					}
					if (env.uibuildresult==0){
						emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
										Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
					}
					if(env.logforwarderbuildresult==0) {
						emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
											Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
					}
					if(env.controlcenterbuildresult==0){
						emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
											Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
					}
					if(env.jimbuildresult==0){
						emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
											Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
					}
				}
			}   
		}
    }  
}
te
