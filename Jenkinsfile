pipeline {
    agent any

    stages {
        stage('Build maven') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
            }
            post {
               always {
                   echo 'One way or another, I have finished'
               }
               success {
                   echo 'I succeeded!'
               }
               failure {
                   echo 'I failed '
               }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                // bat '.\\mvnw test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('Run app') {
            steps {
                sh 'fuser -k 9090/tcp || true'
                sh 'java -jar ./target/demo-0.0.1-SNAPSHOT.jar'
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

    }
}