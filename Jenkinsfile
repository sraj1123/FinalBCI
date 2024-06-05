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
                }
            }
        }

        stage('Quality Gate Check'){
            steps{
                timeout(time: 1, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}