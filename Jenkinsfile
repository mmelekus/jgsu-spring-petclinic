#!/usr/bin/env groovy
// shebang tells most editors to treat as groovy (syntax highlights, formatting, etc...)

pipeline {
    agent any

    // triggers { pollSCM('* * * * *')}

    stages {
        //stage('Checkout') {
        //    steps {
        //        git url: 'https://github.com/mmelekus/jgsu-spring-petclinic.git',
        //        branch: 'main',
        //        credentialsId: 'WSL2Jenkins'
        //    }
        //}

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }

        changed {
            emailext subject: "Job \'${JOB_NAME}\' (build ${BUILD_NUMBER}) ${currentBuild.result}",
                body: "Please go to ${BUILD_URL} and verify the build",
                attachLog: true,
                compressLog: true,
                to: "test@jenkins",
                recipientProviders: [upstreamDevelopers(), requestor()]
        }
    }
}