pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS_USR = "hari-cicd"
	DEPLOY_CREDS_PSW = "Indian@018"
    MULE_VERSION = '4.2.2'
    BG = "IFT"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

 /*   stage('Test') {
      steps {
          bat "mvn test"
      }
    } */

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'timezone-app'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.worker="%WORKER%"'
      }
    }
   /* stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Production'
        APP_NAME = '<API-NAME>'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    } */
	stage('performance test') {
      steps {
             bat  'C:/Users/harikrishnan.pv/Downloads/apache-jmeter-5.2.1/apache-jmeter-5.2.1/bin/jmeter.bat -jjmeter.save.saveservice.output_format=xml -n -t C:/Users/harikrishnan.pv/Downloads/apache-jmeter-5.2.1/apache-jmeter-5.2.1/bin/worldTimeZoneTest.jmx -l C:/Users/harikrishnan.pv/Downloads/apache-jmeter-5.2.1/apache-jmeter-5.2.1/bin/report.jtl'
      }
    }
  }
}