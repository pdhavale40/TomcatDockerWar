// Powered by Infostretch 

timestamps {

node () {

	stage ('Sample-DevOps - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'b5cbc4c0-6b60-4369-872b-2f62a5d494e9', url: 'https://github.com/MyGitHub2907/TomcatDockerWar.git']]]) 
	}
	stage ('Sample-DevOps - Build') {
 			// Maven build step
	withMaven(maven: 'Maven3.8.1') { 
 			if(isUnix()) {
 				sh "mvn clean deploy " 
			} else { 
 				bat "mvn clean deploy " 
			} 
 		} 
	}
}
}