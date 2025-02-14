pipeline {
    agent any

    tools {
        // Ensure Maven is installed and available.
        maven "Maven"
    }

    stages {
        stage('Echo version') {
            steps {
                // Display Maven version
                sh 'echo print maven version'
                sh 'mvn -version'
            }
        }
        stage('Build') {
            steps {
                // Clone the GitHub repository
                // git branch: 'main', url: 'https://github.com/dileepkumaradabala/jenkins-hello-world.git'

                // Build the project using Maven, ignoring test failures
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Unit Test') {
            steps {
                script {
                    for(int i=0;i<60;i++){
                        echo "${i + 1}"
                        sleep 1
                    }
                }
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
