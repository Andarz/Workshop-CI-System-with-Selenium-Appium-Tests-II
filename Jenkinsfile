pipeline {
    agent any

    stages {
        stage("Checkout code") {
            //checkout repository
            steps {
                git branch: 'master', url: 'https://github.com/Andarz/Workshop-CI-System-with-Selenium-Appium-Tests-II'
            }

        }
        stage("Setup .Net Core") {
            //install dotnet
            steps {
                bat '''
                echo Downloading .Net 6.0 Sdk
                curl -L -o dotnet-sdk-6.0.132-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/ad59f1d1-5f19-4474-86be-2f09ab195618/5c7a64445dae84e386bb88e1f6ac09e4/dotnet-sdk-6.0.132-win-x86.exe
                echo Installing .Net Sdk 6.0
                dotnet-sdk-6.0.132-win-x86.exe /quiet /norestart
                '''
            }
            
        }
        stage("Restore dependencies") {
            //install dependencies
            steps {
                bat 'dotnet restore SeleniumIde.sln'
            }
            
        }
        stage("Build") {
            //build
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
            
        }
        stage("Run Tests") {
            //run tests
            steps {
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"'
            }            
        }
    }
}