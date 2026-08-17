pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore src\\GitJenkinsDemo\\GitJenkinsDemo.csproj'
                bat 'dotnet restore tests\\GitJenkinsDemo.Tests\\GitJenkinsDemo.Tests.csproj'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build src\\GitJenkinsDemo\\GitJenkinsDemo.csproj --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test tests\\GitJenkinsDemo.Tests\\GitJenkinsDemo.Tests.csproj --no-restore --configuration Release'
            }
        }

        stage('Publish') {
            steps {
                bat 'dotnet publish src\\GitJenkinsDemo\\GitJenkinsDemo.csproj --no-build --configuration Release --output publish'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'SUCCESS: Build, test and publish completed.'
        }

        failure {
            echo 'FAILED: Please check the Console Output.'
        }
    }
}