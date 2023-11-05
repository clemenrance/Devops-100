pipeline{

    agent any

    stages{

        stage ("Continous Download"){
           steps{
            git branch: 'main', url: 'https://github.com/clemenrance/Devops-100.git'
           }
        }
        stage("Unit Test"){
            
            steps{
                sh 'mvn test'
            }
        }
        stage("Integration Testing"){

            steps{
                sh'mvn verify -DskipUnitTests'
            }
        }
        stage("Continouse Build"){

            steps{
                sh'mvn clean install'
            }
        }
        stage("STATIC TEST ANALYSIS"){

            steps{

                script{
                    withSonarQubeEnv(credentialsId: 'api-sonar'){
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Test Analysis"){

            steps{

                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'api-sonar'
                }
            }
        }
        stage("Upload artifact to Nexus"){

            steps{

                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '3.83.224.93:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Devops-100', version: '1.0.0'
                }
            }
        }
    }
}