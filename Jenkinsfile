node ('master')
{
    def mvnhome = tool name:"maven3.8.4"
	properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
    stage('checkout')
    {
        git credentialsId: 'rajigit', url: 'https://github.com/RDstories/maven-web-application.git'
    }
    stage('build')
    {
        sh "${mvnhome}/bin/mvn clean package"
    }
    stage('QA')
    {
        sh "${mvnhome}/bin/mvn  sonar:sonar"
    }
    stage('nexus')
    {
        sh "${mvnhome}/bin/mvn  deploy"
    }
     stage ('deploy')
     {
       sshagent(['retest']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.2.37.169:/opt/apache-tomcat-9.0.58/webapps"
        }
    }
   /*stage('sendemail')
   {
       mail bcc: '', body: 'chudu chudu chudu devops ne chudu anil ni chusavo peeka kosthaaa', cc: 'rajitha.svtm@gmail.com', from: '', replyTo: '', subject: 'build completuuuuuu naaa pipe success', to: 'lokesh.adriot@gmail.com'
       
   }*/
   
}





/*pipeline{

agent any

tools{
maven 'maven3.8.2'

}

triggers{
pollSCM('* * * * *')
}

options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}

stages{

  stage('CheckOutCode'){
    steps{
    git branch: 'development', credentialsId: '957b543e-6f77-4cef-9aec-82e9b0230975', url: 'https://github.com/devopstrainingblr/maven-web-application-1.git'
	
	}
  }
  
  stage('Build'){
  steps{
  sh  "mvn clean package"
  }
  }
/*
 stage('ExecuteSonarQubeReport'){
  steps{
  sh  "mvn clean sonar:sonar"
  }
  }
  
  stage('UploadArtifactsIntoNexus'){
  steps{
  sh  "mvn clean deploy"
  }
  }
  
  stage('DeployAppIntoTomcat'){
  steps{
  sshagent(['bfe1b3c1-c29b-4a4d-b97a-c068b7748cd0']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.190.162:/opt/apache-tomcat-9.0.50/webapps/"    
  }
  }
  }
  */
//Stages Closing

/*post{

 success{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
 failure{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
}


}//Pipeline closing
*/


