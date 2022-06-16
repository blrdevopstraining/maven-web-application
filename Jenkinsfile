node{
      def mavenHome =  tool name: "maven-3.8.6", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
     
    stage('SCM Checkout'){
        git branch: 'development', credentialsId: 'githubpassword', url: 'https://github.com/blrdevopstraining/maven-web-application.git'
    }
    
    stage(" Maven Clean Package"){

      sh "${mavenCMD} clean package"
      
    }
