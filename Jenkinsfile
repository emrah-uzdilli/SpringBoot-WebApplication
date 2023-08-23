pipeline {
    agent any
    
    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout ') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/emrah-uzdilli/SpringBoot-WebApplication.git'
            }
        }

        stage('Code Compile') {
            steps {
                    sh "mvn compile"
            }
        }

        stage('Run Test Cases') {
            steps {
                    sh "mvn test"
            }
        }

        stage('Sonarqube Analysis') {
            steps {
                    withSonarQubeEnv('sonar-server') {
                        sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Java-WebApp \
                        -Dsonar.java.binaries=. \
                        -Dsonar.projectKey=Java-WebApp '''

                }
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                   dependencyCheck additionalArguments: '--scan ./   ', odcInstallation: 'DP'
                   dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage('Maven Build') {
            steps {
                    sh "mvn clean compile"
            }
        }

        stage('Docker Build & Push') {
            steps {
                   script {
                       withDockerRegistry(credentialsId: '89d444e6-f3c3-4602-b765-d99c550b0cf5', toolName: 'Docker') {
                            sh "docker build -t webapp ."
                            sh "docker tag webapp emrah-uzdilli/webapp:latest"
                            sh "docker push adijaiswal/webapp:latest "
                        }
                   }
            }
        }

        stage('Docker Image scan') {
            steps {
                    sh "trivy image emrah-uzdilli/webapp:latest "
            }
        }

    }
}