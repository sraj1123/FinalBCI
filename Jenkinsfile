pipeline{
    agent any

    tools{
        maven "maven"
    }
    stages{

        stage('Git Clone'){
            steps{
                git branch: 'master', url: 'https://github.com/csiripurapu/mvnproject'
            }
        }

        stage('Maven Build'){
            steps{
                script{
                    sh "mvn clean install"
                }
            }
        }

        stage('Sonar Scan'){
            steps{
                script{
                    withSonarQubeEnv('SQ')
                    sh 'mvn sonar:sonar -Dsonar.projectName=Test2 -Dsonar.projectKey=Test2'
                }
            }
        }
    }
}