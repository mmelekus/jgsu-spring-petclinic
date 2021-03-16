pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mmelekus/jgsu-spring-petclinic.git',
                branch: 'main',
                credentialsId: 'WSL2Jenkins'
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'targe/*.jar'
                }
            }
        }
    }
}