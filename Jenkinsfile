node {
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/koefoed/gildedrose.git'
   }
	stage('Build') {
		withDockerContainer('maven:3-jdk-8'){
			sh 'echo hello world'
			mvn -Dmaven.test.failure.ignore clean package
		}

		//sh 'docker run -i --rm --name my-maven-project -v "$pwd":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn -Dmaven.test.failure.ignore clean package'

		// Run the maven build
		/*
		if (isUnix()) {
		 sh "mvn -Dmaven.test.failure.ignore clean package"
		} else {
		 bat(/"${mvnHome}\bin\mvn" clean package/)
		}
		*/
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
