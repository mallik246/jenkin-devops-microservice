//SCRIPTED
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration Test"
// }

//DECLARATIVE
pipeline {
	agent { docker { image 'node:13.8'} }
	stages{
		stage('Build'){
			steps {
				sh 'node --version'
				echo "Build"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps {
				echo "Integration Test"
			}
		}

	} 
	post {
		always {
			echo 'Im Awsome. I run always'
		}
		success {
			echo 'I run when your successful'
		}
		failure {
			echo 'I run when your failed'
		}		
	}
}