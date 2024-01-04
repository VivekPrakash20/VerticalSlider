pipeline{
    agent any
    stages{
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
