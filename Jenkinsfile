pipeline {
    agent any
    environment {
        SCALA_VERSION = "2.12.4"
        SCALA_HOME = "/usr/share/scala"
    }
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/jglick/simple-maven-project-with-tests.git'

                // Run Maven on a Unix agent.
                sh "sbt -Dsbt.log.noformat=true clean dist"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {

                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
