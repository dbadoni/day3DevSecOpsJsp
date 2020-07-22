pipeline {

agent any

tools {
	maven 'maven'
}

stages {
	stage('checkcing maven installation'){
		steps {
			sh 'mvn -v'
		}
	}
	stage('security checking by trufflehog'){
		steps {
			sh 'docker run --rm gesellix/trufflehog --json https://github.com/dbadoni/day3DevSecOpsJsp.git >mybugs.txt'
			sh 'cat mybugs.txt'
		}
	}
	stage('vulner by sonar'){
		steps {
			withSonarQubeEnv('sonar'){
				sh 'mvn sonar:sonar'
				sh 'cat target/sonar/report-task.txt'
			}
			
		}
	}
	
	stage('build java project'){
		steps {
			sh 'mvn clean package'
		}
	}


}
}

