pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                powershell 'dotnet restore' 
                powershell 'dotnet build --no-restore' 
            }
        }
    }
}