pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                powershell 'dotnet restore' 
                powershell 'dotnet build --no-restore' 
            }
        }
        stage('Test') {
            steps {
                powershell 'dotnet test --no-build --no-restore --collect "XPlat Code Coverage"'
            }
            post {
                always {
                    recordCoverage(tools: [[parser: 'COBERTURA', pattern: '**/*.xml']], sourceDirectories: [[path: 'SimpleWebApi.Test/TestResults']])
                }
            }
        }
    }
}