#!/usr/bin/env groovy

pipeline {
    agent any
    
    tools{
        maven "Maven"
    }
    
    stages{
     
        stage("Fetching"){
            steps{
                echo "Fetching the code"
                git branch: "main", url: "https://github.com/testgit4me/cicd-jenkins.git"
            }
        }
        stage("Building"){
            steps{
                echo "Building the jar file"
                sh "mvn install"
            }
        }
        stage("Tesing"){
            steps{
                echo "Tesing the jar & GIT file2"
                echo "Tesing the jar & GIT file2"
                sh "mvn test"
            }
        }
        
        stage('MVN Checkstyle'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }

        // stage('Sonar Analysis') {
        //     environment {
        //         scannerHome = tool 'sonar4.7'
        //     }
        //     steps {
        //        withSonarQubeEnv('sonar') {
        //            sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
        //            -Dsonar.projectName=vprofile \
        //            -Dsonar.projectVersion=1.0 \
        //            -Dsonar.sources=src/ \
        //            -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
        //            -Dsonar.junit.reportsPath=target/surefire-reports/ \
        //            -Dsonar.jacoco.reportsPath=target/jacoco.exec \
        //            -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
        //       }
        //     }
        // }

        stage("Uploading artifact"){
            steps{

                echo "Uploading jar file to Nexus repository"

                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '172.31.9.99:8081',
                    groupId: '',
                    version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                    repository: 'app-pipeline',
                    credentialsId: 'nexusLogin',
                    artifacts: [
                        [artifactId: boxfuse,
                        classifier: '',
                        file: 'target/hello-1.0.war',
                        type: 'war']
                        ]
                )
            }
        }       
    }    
}