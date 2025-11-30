//scripted

//declarative
pipeline{
	agent any
	// agent { docker { image 'maven:3.6.3'}}
	environment{
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		// PATH = "$dockerHome/bin:$PATH"
	}
	stages {
		stage('Build'){
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "Build_ID - $env.BUILD_ID"
			}
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}		
		stage('Test'){
			steps {
				sh "mvn Test"
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
		stage('Build Docker Image'){
			steps {
				script{
					dockerImage = docker.build("tush3112/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('push Docker Image'){
			steps {
				script{
					docker.withRegistry('',dockerhub){
						dockerImage.push()
						dockerImage.push('latest');
					}
				}
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
