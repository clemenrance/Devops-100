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
    }
}