pipeline {
    agent {
        node {
            label 'build'
        }
    }
environment {
    PATH = "/opt/maven/bin:$PATH"
}
    stages { 
        stage("Build"){
            steps {
                 echo "----------Build Maven Started----------"
                 sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
       }
        stage("Unit Test") {
           steps {
                 echo "----------Unit Test Started----------"
                 sh 'mvn surefire-report:report'
            }
        }
        stage("SonarQube") {
        environment {
            scannerHome = tool 'sonarqube_scanner'
        }
        steps{
        withSonarQubeEnv('sonarqube_server') {
            sh "${scannerHome}/bin/sonar-scanner"
            }
        }
        } 
    }
}
