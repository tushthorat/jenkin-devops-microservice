//scripted

//declarative
pipeline{
	agent any
	// agent { docker { image 'maven:3.6.3'}}
	environment{
		dockerHome = tool 'myDocker'
		// mavenHome = tool 'myMaven'
		// PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		PATH = "$dockerHome/bin:$PATH"
	}
	stages {
		stage('Build'){
			steps {
				// sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "Build_ID - $env.BUILD_ID"
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
	post{
		always{
			echo 'im awesome. I run always'
		}
		success{
			echo 'i run when you are successful'
		}
		failure{
			echo 'i run when you fail'
		}
	}
}








node {
		echo "Build"
		echo "Test"
		echo "Integration Test"

}
