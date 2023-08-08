pipeline {
    agent {
        node {
            label 'build'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.2/bin:$PATH"
}
    stages {
        stage("build"){
            steps {
                 echo "----------Building Maven----------"
                 sh 'mvn clean deploy'
            }
       }
    } 
}
