pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('checkout'){steps {git credentialsId: 'githubcred', url: 'https://github.com/abhibade9/java-db-Login.git'}}
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                deploy adapters: [tomcat8(credentialsId: 'tomcatcred', path: '', url: 'http://54.234.178.253:9080/')], contextPath: 'login', war: '**/*.war'
                }
            }
        }
    }
}
