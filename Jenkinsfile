node('') {
	def sonarScanner = tool name: 'forSonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	stage ('checkout code'){
		checkout scm
	}
	
	stage ('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}

	stage ('Test Cases Execution'){
		sh "mvn clean test"
	}

        stage('SonarQube Analysis'){
          withSonarQubeEnv(credentialsId: 'sonarCred') {
           sh "${sonarScanner}/bin/sonar-scanner -Dsonar.projectKey=hello-world -Dsonar.sources=."
            } 
        }

// 	stage ('Archive Artifacts'){
// 		archiveArtifacts artifacts: 'target/*.war'
// 	}
	
// 	stage ('Deployment'){
// 		ansiblePlaybook colorized: true, disableHostKeyChecking: true, playbook: 'deploy.yml'
// 	}
	
// 	stage ('Notification'){
// 		emailext (
// 		      subject: "Job Completed",
// 		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
// 		      to: "build-alerts@example.com"
// 		    )
//	}
}
