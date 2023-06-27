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
          bat "nexusPublisher nexusInstanceId: 'Nexus', nexusRepositoryId: 'test', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target\\test-1.0-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'test', groupId: 'com.test.project', packaging: 'jar', version: '1.0']]], tagName: '1.0.0'"
        }
      }
    }
}
