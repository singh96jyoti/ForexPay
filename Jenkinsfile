pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/singh96jyoti/ForexPay.git'
		}
	}
	stage('Build') {
		steps {
			withSonarQubeEnv('sonar') {
				sh '/usr/share/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'
			}
		}
	}
	stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
       
	stage ('Deploy') {
		steps {
			
			sh '/usr/share/maven/bin/mvn clean deploy -Dmaven.test.skip=true'
		}
	}
}
	

}
