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
                 echo "---------------MAVEN BUILD STARTED---------------"
                 sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
       }
        stage("Unit Test") {
           steps {
                 echo "-------------UNIT TEST STARTED---------------"
                 sh 'mvn surefire-report:report'
            }
        }
        stage("SonarQube") {
        environment {
            scannerHome = tool 'sonarqube_scanner'
        }
            steps{
                echo"---------------SONARQUBE STARTED---------------"
                withSonarQubeEnv('sonarqube_server') {
                sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        } 
        stage("Quality Gate") {
            steps {
                echo"---------------QUALITY GATE STARTED---------------"
                script {
                    timeout(time: 1, unit: 'HOURS') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to Quality Gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}
