pipeline {
    agent any

    tools {
        // Ensure Maven is installed and available.
        maven "Maven"
    }

    stages {
        stage('gitwebhook'){
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/dileepkumaradabala/jenkins-hello-world.git']])
            }
        }
        stage('Build') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'https://github.com/dileepkumaradabala/jenkins-hello-world.git'

                // Build the project using Maven, ignoring test failures
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Unit Test') {
            steps {
                // Run unit tests using Maven
                sh 'mvn test'
            }
        }
    }

    post {
        success {
            // Archive test results and JAR file on successful build
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts artifacts: 'target/*.jar', onlyIfSuccessful: true
        }
    }
}
