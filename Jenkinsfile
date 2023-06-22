pipeline {
    agent any
    stages { 
      stage('checkout SCM') {
        steps {
          bat "git pull https://github.com/srinivas-0/maven.git"
          }
      }
      stage('package') {
        steps {
          bat "mvn clean package"
        }
      }
      stage('Static Analysis') {
        steps {
          withSonarQubeEnv('sonarqube') {
            bat "mvn sonar:sonar -Dsonar.projectKey=sample-demo"
          }
        }
      }
    }
}
