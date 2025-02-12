pipeline {
    agent any
    tools {
        nodejs 'nodejs-22-6-0' // Name from "Global Tool Configuration"
    }
    stages {
        stage('Installing Dependecies') {
            steps {
                sh 'npm install --no-audit'
            }
        }
    }
}
