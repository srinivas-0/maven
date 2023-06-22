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
              bat "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar"
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
