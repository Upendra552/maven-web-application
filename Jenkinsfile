node('master'){

  def mvnHome = tool name: 'Maven', type: 'maven'
  def mvnBIN= "${mvnHome}/bin"
  cleanWs notFailBuild: true
  currentBuild.result = "SUCCESS"
  
  
  
  stage('checkout'){
 git branch: 'development', credentialsId: 'e43d7eb1-9665-452e-8ead-52821a402d9f', url: 'https://github.com/Upendra552/maven-web-application.git'
  }
  stage('build'){
     if(isUnix()){
     sh "${mvnBIN}/mvn clean package sonar:sonar"
      }
      else{
       bat "${mvnHome}/bin/mvn clean package"   
      }
   }
   /*
   stage('sonarqubereport'){
     if(isUnix()){
     sh '${mvnBIN}/mvn sonar:sonar'
      }
      else{
       bat 'mvn sonar:sonar'   
      }
  }
  */
  
  stage('DeployAppIntoTomcat'){
     if(isUnix()){
	  sh 'echo "Starting deployment"'
      sh 'scp $WORKSPACE/target/*.war /opt/apache-tomcat-9.0.14/webapps'
      sh 'echo "Deployment done successfully"'
	  }
      else{
       bat 'echo windows'   
      }
  }
  stage('upload nexus'){
      if (isUnix()){
          sh 'mvn deploy'
      }else{
          bat 'mvn deploy'
      }
        
      
  }
  
 
 stage('emailnotification'){
  	      mail  to: 'm.upendra14@gmail.com', 
		        cc: 'm.upendra14@gmail.com', 
				
				from: 'm.upendra14@gmail.com', 
				replyTo: 'm.upendra14@gmail.com',             
				subject: 'Project build Succeed',
				body: 'Buid Done'
  
    
  	   }
}
