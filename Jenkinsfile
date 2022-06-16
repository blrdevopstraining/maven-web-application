node{
      def mavenHome =  tool name: "maven-3.8.6", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
     
    stage('SCM Checkout'){
        git credentialsId: 'github', url: 'https://github.com/blrdevopstraining/java-web-app-docker.git'
    }
    
    stage(" Maven Clean Package"){

      sh "${mavenCMD} clean package"
      
    }
