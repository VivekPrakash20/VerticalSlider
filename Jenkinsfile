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
                          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.101.16.44:9090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
