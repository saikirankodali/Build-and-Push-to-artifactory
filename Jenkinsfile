pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3.9.8"
    }

    stages {
        stage('Clone the repository') {
            steps {
                git 'https://github.com/techworldwithmurali/Build-and-Push-to-artifactory.git'
            }
        }
        
        stage('Build and test the application') {
            steps {
                sh 'mvn clean test'
                sh 'mvn surefire-report:report'
            }
        }
        
        stage('clean-install') {
            steps {
               sh 'mvn clean install'
            }
        }

        stage('maven deploy') {
            steps {
             deploy adapters: [tomcat9(credentialsId: 'Tomcat_admin', path: '', url: 'http://34.216.240.43:8080/')], contextPath: null, war: '**/*.war'
          }    
        }
    }
}
