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
      stage('test') {
        steps {
          bat "mvn clean test"
        }
      }
      stage('publish to nexus') {
        steps {
          nexusArtifactUploader artifacts: [
              [
                  artifactId: 'test',
                  clasifier: '',
                  file: 'C:/ProgramData/Jenkins/.jenkins/workspace/sample-pipeline/target/*.jar',
                  type: 'jar'
              ]
            ],
            credentialsId: 'nexus',
            groupId: 'com.test.project',
            nexusUrl: 'localhost:8081',
            nexusVersion: 'nexus3',
            protocol: 'http',
            repository: 'http://localhost:8081/repository/test/',
            version: '1.0'
        }
      }
    }
}
