pipeline {
    agent any
//     environment {
//         SCALA_VERSION = "2.12.4"
//         SCALA_HOME = "/usr/share/scala"
//     }
    stages {
//         stage('Setting Up'){
//             steps {
//                 sh 'apk add --no-cache --virtual=.build-dependencies wget ca-certificates '
//                 sh 'apk add --no-cache bash curl jq '
//                 sh 'cd "/tmp" '
//                 sh 'wget --no-verbose "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" '
//                 sh 'tar xzf "scala-${SCALA_VERSION}.tgz" '
//                 sh 'mkdir "${SCALA_HOME}" '
//                 sh 'rm "/tmp/scala-${SCALA_VERSION}/bin/"*.bat '
//                 sh 'mv "/tmp/scala-${SCALA_VERSION}/bin" "/tmp/scala-${SCALA_VERSION}/lib" "${SCALA_HOME}" '
//                 sh 'ln -s "${SCALA_HOME}/bin/"* "/usr/bin/" '
//                 sh 'apk del .build-dependencies '
//                 sh 'rm -rf "/tmp/"* '
//             }
//         }
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
