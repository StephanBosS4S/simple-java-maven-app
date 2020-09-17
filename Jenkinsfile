node {
 def mvnHome
 stage('SCM Checkout') { // for display purposes
  // Get some code from a GitHub repository
   git 'https://github.com/StephanBosS4S/simple-java-maven-app'
  // Get the Maven tool.
  // ** NOTE: This 'M3' Maven tool must be configured
  // **       in the global configuration.           
   mvnHome = tool 'maven3'
 }
 stage('Build') {
  // Run the maven build
  if (isUnix()) {
     sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
  } else {
     bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
  }
}
stage('Test')   {
   //Perform test
   echo 'Execute the script'
    if (isUnix()) {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test"
  } else {
     bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore test/)
  }

 }
 stage('Results') {
  junit '**/target/surefire-reports/TEST-*.xml'
  archiveArtifacts 'target/*.jar'
}
 stage('Email Notification'){
    mail bcc: '', body: 'Dit is een test', cc: '', from: '', replyTo: '', subject: 'Jenkins test', to: 'stephanboshu@gmail.com'
 }
 
 stage('slack bericht'){
  slackSend baseUrl: 'https://hooks.slack.com/services/', channel: 'test', color: 'good', message: 'Hello, this is a test!', teamDomain: 'Search4Solutions', tokenCredentialId: 'Slack'
 }
 
 stage('SonarQube Analysis') {
        withSonarQubeEnv('sonar') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
 
 stage('Nexus') {
       //  
          //
        }
    }
//}
