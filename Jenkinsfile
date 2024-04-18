pipeline{
    agent any
    tools{
        maven 'local_maven'
    }

    stages{
        stage ('Build') {
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/targets/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat7(credentialsId: '627eb692-421d-4282-8432-ccb62b97855e', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'

            }
        }
    }
}