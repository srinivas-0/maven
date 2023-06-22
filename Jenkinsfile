pipeline {
    agent any
    stages { 
        stage('checkout SCM') {
            steps {
              bat "git pull https://github.com/srinivas-0/maven.git"
            }
        }
        stage('Static Analysis') {
            steps {
              withSonarQubeEnv('sonarqube')
              bat "mvn clean sonar:sonar"
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
