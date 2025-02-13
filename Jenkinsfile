pipeline {
    agent any
    tools {
        nodejs 'Node-22-6-0' // Name from "Global Tool Configuration"
    }
    environment {
        MONGO_URI = "mongodb+srv://supercluster.d83jj.mongodb.net/superData"
    }

    stages {
            stage('Installing Dependecies') {
                steps {
                    sh 'npm install --no-audit'
                }
            }
            stage('Dependecy Scanning') {
                parallel{
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
                --prettyPrint''', odcInstallation: 'OWASP-DeepCheck-12-0-2'

                dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true

                junit allowEmptyResults: true, stdioRetention: '', testResults: 'dependency-check-junit.xml'

                publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, keepAll: true, reportDir: './', reportFiles: 'dependency-check-jenkins.html', reportName: 'Dependency Check HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                }
            }
        }
    }   

    stage('Unit Testing') {
                steps {
            withCredentials([usernamePassword(credentialsId: 'mongo-cred', passwordVariable: 'MONGO_PASSWORD', usernameVariable: 'MONGO_USERNAME')]) {
            sh 'npm test'
        }
        junit allowEmptyResults: true, stdioRetention: '', testResults: 'test-result.xml'
                            
      }
    }
}
  


  /*   stages {
        stage('Installing Dependecies') {
            steps {
                sh 'npm install --no-audit'
            }
        }

        stage('Dependecy Scanning') {
            parallel{
        stage('NPM Dependecy Audit') {
            steps {
                sh '''
                  npm audit --audit-level=critical
                  echo $?
                '''
            }
        }
    }
 }
} */


}
