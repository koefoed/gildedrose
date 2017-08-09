node {
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/koefoed/gildedrose.git'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "mvn -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" clean package/)
      }
   }
   stage('Javadoc'){
       sh "mvn site"
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
      archive 'target/javadoc'
   }
}
