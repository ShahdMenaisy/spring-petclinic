pipeline {
    agent any

    tools {
        maven 'maven3.9.15'
        jdk 'jdk'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }

        stage('Change Config') {
            steps {
                sh 'echo "server.port=9092" >> src/main/resources/application.properties'
            }
        }

        stage('Maven Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Maven Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Maven Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Maven Run') {
            steps {
                sh '''
                    nohup java -jar target/*.jar > app.log 2>&1 &
                    sleep 100
                '''
            }
        }
    }
}
