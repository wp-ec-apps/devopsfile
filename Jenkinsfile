node

{

def mavenHome = tool name: "maven3.6.3"

 stage('Checkoutcode')
  {
	git branch: 'development', credentialsId: '3e2e715d-15f6-4aa1-aec3-70ce3e6bcd26', url: 'https://github.com/wp-ec-apps/maven-web-application.git'
  }
  
  stage ('Build')
  {
	 sh "${mavenHome}/bin/mvn clean package"
  }
  
  stage ('ExecuteSonarQubeReport')
  { 
	sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  
  stage('UploadArtifcatInNexus')
  {
	sh "${mavenHome}/bin/mvn deploy"
  }
  stage('DeploytoTomcat')
  {
	sshagent(['TomacatServerLinuxCredentials']) 
	{
		sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.215.245:/opt/apache-tomcat-9.0.38/webapps"
	}
  }
   
 }
