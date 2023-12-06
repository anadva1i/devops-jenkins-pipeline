pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    stages {
        stage('Clone') {
            steps {
                git branch:'main', url: 'https://github.com/ttutberidze/react-iliauni-2023-fall.git'
            }
        }
        stage('Install') {
            steps {
                sh 'cd 3 && npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'cd 3 && npm run build'
            }
            post {
                success {
                    archiveArtifacts artifacts: '3/build/*'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'cd 3 && npm run test'
            }
        }
        stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'sonar-tool'
            }
            steps {
               withSonarQubeEnv('sonar-server') {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=react-app \
                   -Dsonar.projectName=react-app \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=3/src/'''
              }
            }
        }
        
    }
}