
node('flipkart-node')
{
    
     //Getting the  env  global varibale values
 
  echo "GitHub BranhName ${env.BRANCH_NAME}"
  echo "Jenkins Job Number ${env.BUILD_NUMBER}"
  echo "Jenkins Node Name ${env.NODE_NAME}"
  
  echo "Jenkins Home ${env.JENKINS_HOME}"
  echo "Jenkins URL ${env.JENKINS_URL}"
echo "JOB Name ${env.JOB_NAME}"
   def mvnHome = tool name: 'maven3.6.1', type: 'maven'
   
     properties([
       buildDiscarder(logRotator(numToKeepStr: '5')),
       pipelineTriggers([
           pollSCM('* * * * *')
       ])
   ])
   
   
   stage('checkoutcodefromgithub'){
       
      git branch: 'development', credentialsId: 'e93bf3fe-9b64-42dd-b45c-2da9cafeedf1', url: 'https://github.com/blrdevopstraining/maven-web-application.git' 
   } 
    
    
    stage('Build'){
        
      sh "${mvnHome}/bin/mvn clean package"
	 
    }
    stage('SonarQubeReport'){
	
	sh "${mvnHome}/bin/mvn clean sonar:sonar"
	
	}
	
	stage('UploadArtifacts'){
	
	sh "${mvnHome}/bin/mvn clean deploy"
	
	}
	
	stage('DeployApplication'){
	
	sshagent(['sshkeyagenttomcat']) {
	    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.115.195:/opt/apache-tomcat-9.0.22/webapps/maven-web-application.war"
	}
	}
	
	stage('EmailNotification'){
	    emailext body: '''Build Mail from Jenkins

Regards,
MSS''', subject: 'Test Mail', to: 'blrdevopstraining@gmail.com'
	}
    
}
