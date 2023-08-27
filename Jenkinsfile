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
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-scanner') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Java-WebApp \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=Java-WebApp'''
        }
    }
}

         stage('OWASP Dependency Check') {
            steps {
                   dependencyCheck additionalArguments: '--scan ./ --format HTML ', odcInstallation: 'DP'
                   dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

          stage('Maven Build') {
            steps {
                    sh "mvn clean install"
            }
        }
         stage('Docker Build') {
            steps{
                script{
                    sh "docker build -t webapp ."
                    sh "docker tag webapp emrahuzdilli/webapp:latest"
            }
          }
        }

        stage('Docker Push') {
            steps {
                   script {
                       withCredentials([string(credentialsId: 'Dockerhub-pwd', variable: 'dockerhubpwd')]) {
                            sh "docker login -u emrahuzdilli -p ${dockerhubpwd}"
                            sh "docker push emrahuzdilli/webapp:latest "
                        }
                   }
            }
        }
         stage('TRIVY Image Scanner') {
            steps {
                    sh "trivy image emrahuzdilli/webapp:latest"
            }
        }
        stage('CD Trigger') {
            steps {
                    build job:"AutomationVulnerabilities_CD" , wait:true
            }
        }


    }
}