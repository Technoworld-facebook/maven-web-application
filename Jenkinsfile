node 
{
def mavenHome = tool name:"maven3.8.5"
stage ('CheckoutCode')
{
git branch: 'development', credentialsId: 'dda2ba4f-b0f0-4046-bb90-4623806c0452', url: 'https://github.com/Technoworld-facebook/maven-web-application.git'
}

stage ('Build')
{
sh "$mavenHome/bin/mvn clean package"
}

stage ('ExecuteSonarQubeReport')
{
sh "$mavenHome/bin/mvn sonar:sonar"
}

stage ('UploadArtifactIntoNexus')
{
sh "$mavenHome/bin/mvn deploy"
}

stage ('DeployAppIntoTomcat')
{
sshagent(['a31d71da-d73c-4bbd-80f4-589fa2a59a22']){
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@52.66.150.217:/opt/apache-tomcat-9.0.59/webapps/"
}
}

  
}//node closing
