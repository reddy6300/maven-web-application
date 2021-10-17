node
{
  def mavenHome = tool name: "maven3.6.2"
  stage('checkoutcode'){
git branch: '/master', credentialsId: '138f5d03-8f27-461a-a461-4e1bc350b4f1', url: 'https://github.com/reddy6300/maven-web-application.git'
}

stage('build'){
sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarqubeReport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('uploadArtifactintoNexusRepo'){
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('deploytheAppIntoTomcat')
{
 sshagent(['138f5d03-8f27-461a-a461-4e1bc350b4f1']) { 
sh "scp -o strictHostKeyChecking=no target/maven-web-application.war ec2-user@52.15.220.178:/opt/apache-tomcat-9.0.53/webapps"   
 }    
 }

}//closing brancket for Node
