pipeline {
    agent any 
    tools { 
        maven 'maven' 
      
    }
stages { 
     
 stage('Preparation') { 
     steps {
// for display purpose

      // Get some code from a GitHub repository

      git 'https://github.com/anilkumarpuli/game-of-life.git'

      // Get the Maven tool.
     
 // ** NOTE: This 'M3' Maven tool must be configured
 
     // **       in the global configuration.   
     }
   }

   stage('Build') {
       steps {
       // Run the maven build

      //if (isUnix()) {
         sh 'mvn -Dmaven.test.failure.ignore=true install'
      //} 
      //else {
      //   bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
       }
//}
   }
 
 // stage('Unit Test Results') {
   //   steps {
     // junit '**/target/surefire-reports/TEST-*.xml'
      
      //}
 //}
// stage('Sonarqube') {
  //  environment {
    //    scannerHome = tool 'sonarqube'
   // }
    //steps {
      //  withSonarQubeEnv('sonarqube') {
        //    sh "${scannerHome}/bin/sonar-scanner"
        //}
        //timeout(time: 10, unit: 'MINUTES') {
          //  waitForQualityGate abortPipeline: true
       // }
   // }
//}
     stage('Artifact upload') {
      steps {
     nexusPublisher nexusArtifactUploader credentialsId: '117a3dc3-3cf4-4dee-ad9a-b6a7cb6e326a', groupId: 'pipeline', nexusUrl: 'http://13.126.154.182:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'pipline', version: 'nexus2'
      }
 }
    stage('Deploy War') {
      steps {
        sh label: '', script: 'ansible-playbook deploy.yml'
      }
 }
}
//post {
    //    success {
      //      archiveArtifacts 'gameoflife-web/target/*.war'
        //}
       // failure {
         //   mail to:"sankar.dadi@qentelli.com", subject:"FAILURE: ${currentBuild.fullDisplayName}", body: "Build failed"
        //}
    //}       
}
