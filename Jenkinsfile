pipeline{
    agent any
    stages{
stage ('code compile'){
            steps{
                sh 'mvn compile'
            }
        }
         stage ('code test'){
            steps{
                sh 'mvn test'
            }
        }

          stage ('code QA'){
            steps{
                sh 'mvn pmd:pmd'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo 'Archiving Artifacts'
                    archiveArtifacts artifacts:'**/target/*.war'
                }
            }

        }
        stage("Deploy into tomcat"){
            steps{
                         deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.129.5.85:8000/')], contextPath: null, war: '**/*.war'
            }
        }
         stage('Send Email Notification') {
            steps {
                emailext subject: 'Build Notification',
                          body: 'The build is successful. Your application is deployed.',
                          recipientProviders: [[$class: 'CulpritsRecipientProvider']]
            }
         }
    }
}
