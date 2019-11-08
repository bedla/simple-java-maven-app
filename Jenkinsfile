pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Download dependencies') {
            steps {
                sh 'mvn -B -s .settings.xml dependency:go-offline'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -o -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -o test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
