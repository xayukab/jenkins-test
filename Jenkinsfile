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
            script{
                while read line
                do
                    echo $line | grep -q BUILD_NUMBER
                    if [ $? -eq 0  ];then
                        build_number=`echo $line | awk -F"=" '{print $2}' `
                        appname=`echo $line | awk -F"=" '{print $1}' | awk -F"." '{print $2}'`
                        if [ appname="PIPELINE_BUILD_NUMBER"] || [ appname="GRPC_BUILD_NUMBER" ] || [ appname="TRANSACTIONBROKER_BUILD_NUMBER" ] || [ appname="COMPONENT_AGENT_BUILD_NUMBER" ];then
                            curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/Appsone-2.0/build_number/ | grep -q "ERROR 404"
                            if [ $? -eq 0 ];then
                                emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
                                Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
                            fi   
                        elif [ appname="UI_BUILD_NUMBER" ]
                            curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/appsone-ui-service/build_number | grep -q "ERROR 404"
                            if [ $? -eq 0 ];then
                                emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
                                Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
                            fi
                        elif [ appname="LOGFORWARDER_BUILD_NUMBER" ];then
                            curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/log-forwarder/build_number | grep -q "ERROR 404"
                            if [ $? -eq 0 ];then
                                emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
                                Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
                            fi
                        elif [ appname="CONTROL_CENTER_BUILD_NUMBER" ];then
                            curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/appsone-controlcenter/65 | grep -q "ERROR 404"
                            if [ $? -eq 0 ];then
                                emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
                                Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
                            fi
                        elif [ appname="JIM_BUILD_NUMBER" ];then
                            curl -u appnomic-admin:appnomic@123 http://192.168.13.39:8080/job/Java-Intrusive-Agent/81 | grep -q "ERROR 404"
                            if [ $? -eq 0 ];then
                                emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
                                Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'abhishek.d@appnomic.com'
                            fi
                        fi   
                    fi
                done < modulelist
            }
        }
        
    }
}
