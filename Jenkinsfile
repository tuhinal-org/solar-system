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
        stage('NPM Dependecy Audit') {
            steps {
                sh '''
                  npm audit --audit-level=critical
                  echo $?
                '''
            }
        }
        stage('OWASP Dependency Check') {
        steps {
            dependencyCheck additionalArguments: '''
            --scan \'./\'
            --out \'./\'
            --format \'ALL\'
            --prettyPrint''', odcInstallation: 'OWASP-DeepCheck-12'
        }
}
    }
}
