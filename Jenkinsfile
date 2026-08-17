pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore GitJenkinsDemo.sln'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build GitJenkinsDemo.sln --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test GitJenkinsDemo.sln --no-build --configuration Release'
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