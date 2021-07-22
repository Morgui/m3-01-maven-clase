pipeline {
    agent any
    tools {
        maven "maven3.8.1"
        jdk "jdk16"
    }
    stages {
        stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Sonar') {
           steps {
               sh 'mvn verify sonar:sonar -Dsonar.projectKey=Morgui_m3-01-maven-clase -Dsonar.organization=morgui -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=9a84ea1d292eed35e7726e38e8a4a86b89390f4c -Dsonar.branch.name=master'
           }
        }
    }
}