pipeline {
    agent any
    tools {
        nodejs 'nodejs-22-6-0' // Name from "Global Tool Configuration"
    }
    stages {
        stage('VM Node Version') {
            steps {
                sh '''
                    node -v
                    npm -v
                '''
            }
        }
    }
}
