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
                          deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://18.144.126.156:9090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
