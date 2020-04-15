//SCRIPTED
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration Test"
// }

//DECLARATIVE
pipeline {
	agent any
	// agent { docker { image 'node:13.8'} }

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage('Checkout'){
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Checkout"
			}
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package'){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps {
				//"docker build -t mbhuiyan13/currency-exchange-devops:$evn.BUILD_TAG"
				script {
					dockerImage = docker.build("mbhuiyan13/currency-exchange-devops:${evn.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}

	} 

}