pipeline {
		agent any
		tools {
			maven "maven"
		}
		stages {
				stage('Git Clone') {
				steps {
					// Get code from a GitHub repository
					git branch: 'main', url: 'https://github.com/sraj1123/FinalBCI'
					}
				}
				stage('Maven Build') {
				steps {
					script {
					// Build Maven Code
					sh "mvn clean install"
						}
					}
				}
				stage('Sonar Scan') {
					steps {
						script {
						withSonarQubeEnv(credentialsId: 'SonarQube_Token') {
						sh 'mvn sonar:sonar -Dsonar.projectName=Test2 -Dsonar.projectKey=Test2'
								}
							}
						}
					}
				stage('Quality Gate Check') {
					steps {
						timeout(time: 10, unit: 'MINUTES') {
							waitForQualityGate abortPipeline: false
							}
						}
					}   
			}
	}
