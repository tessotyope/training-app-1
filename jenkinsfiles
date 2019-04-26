node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/tessotyope/training-app-1'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven 3'
   }
   stage('Test') {
      if (isUnix()) {
        
      } else {
         bat(/"${mvnHome}\bin\mvn" clean test/)
    }
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -B -DskipTests -Dmaven.test.failure.ignore package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
   stage('Publish Artefact') {
       
       if (isUnix()) {
                 } else {
           bat(/"${mvnHome}\bin\mvn" -DdeployOnly deploy -s "C:\apache-maven-3.6.0\conf\settings.xml"/) 
       }
   }

   stage('Execute Jar') {
       if (isUnix()) {
           sh "java -jar target/*.jar"
       } else {
           bat(/java -jar target\/training-app-1.0-jar-with-dependencies.jar/)
         }
       }
   
}
