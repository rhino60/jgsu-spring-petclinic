pipeline {
    agent any

    triggers { pollSCM('* * * * *') }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rhino60/jgsu-spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                // To run Maven on a Windows agent, use
                bat "./mvnw.cmd spring-javaformat:apply clean package"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
