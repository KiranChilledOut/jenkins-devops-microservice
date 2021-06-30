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
		stage('Checkout') {
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
		stage("Compile"){
			steps{
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

				stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				// docker build -t chilledout/jenkins-ci-cd:$env:BUILD_TAG
				script{
					dockerimage=docker.build("chilledout/jenkins-ci-cd:${env:BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry("","dockerhub"){
						dockerimage.Push();
						dockerimage.Push('latest')
					}
				}
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