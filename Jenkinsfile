pipeline {
    agent any
    stages { 
        stage('checkout SCM') {
            steps {
              bat "git pull https://github.com/srinivas-0/test.git"
            }
        }
        stage('Compile') {
          steps {
            bat "mvn clean compile"
          }
        }
        stage('Test') {
          steps {
            bat "mvn clean test"
          }
        } 
        stage('package') {
          steps {
            bat "mvn clean package"
          }
        } 
    }
}
