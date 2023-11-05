pipeline{

    agent any

    stages{

        stage ("Continous Download"){
           steps{
            git branch: 'main', url: 'https://github.com/clemenrance/Devops-100.git'
           }
        }
        stage("Integration Testing"){
            
            steps{
                sh 'mvn test'
            }
        }
    }
}