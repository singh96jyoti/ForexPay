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
	       
	stage ('Deploy') {
		steps {
			sh '/usr/share/maven/bin/mvn clean deploy -Dmaven.test.skip=true'
		}
	}
		stage ('Release') {
		steps {
			sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'
		}
	}
}
	

}
