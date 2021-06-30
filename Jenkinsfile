//SCRIPTED Pipeline
// node {
// 	// stage('Build') {
// 	// 	echo "Build"
// 	// }
// 	// stage('Test') {
// 	// 	echo "Test"
// 	// }
// 	// stage('Integration Test') {
// 	// 	echo "Test"
// 	// }
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration Test"
// }

//DECLARATIVE PIPELINE

pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3' } }
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH="/$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Build') {
			steps {
				// echo "$dockerHome"
				echo "$mavenHome"
				sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "$PATH"
				echo "Build number = $env.BUILD_NUMBER"
				echo "build Job = $env.JOB_NAME"
				echo "Build Tag = $env.BUILD_TAG"
				echo "Build ID= $env.BUILD_ID"
				echo "${env.BUILD_URL}"

			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	}
	post {
		always {
			echo "I run always"
		}
		success {
			echo "I run only on success"
		}

		failure {
			echo "I run only on failure"
		}
		//changed
		//

	}
}