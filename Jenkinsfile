pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deploy to tomcat server'){
            steps {
                deploy adapters: [tomcat7(credentialsId: 'GIT_Credential', path: '', url: 'http://100.27.70.115:8081/')], contextPath: null, war: '**/*.war'
            }
                
            
        }
    }
}