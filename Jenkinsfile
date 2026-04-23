pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
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
        stage('Deliver') {
            steps {
                powershell 'dotnet publish SimpleWebApi --no-restore -o published'
            }
            post {
                success {
                    archiveArtifacts 'published/*.*'
                }
            }
        }
    }
}