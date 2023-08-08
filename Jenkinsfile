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
        stage("build"){
            steps {
                 echo "----------Building Maven----------"
                 sh 'mvn clean deploy'
            }
       }
    } 
}
