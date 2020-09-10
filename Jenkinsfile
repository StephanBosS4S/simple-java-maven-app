node { //test
	stage('SCM Checkout'){
		git 'https://github.com/StephanBosS4S/daoCD'
	}
	stage('Build'){
	// get maven home path
	def mvnHome = tool name: 'maven3', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
}
