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
                 echo "----------Building Maven----------"
                 sh 'mvn clean deploy'
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
