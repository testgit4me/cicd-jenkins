#!/usr/bin/env groovy

pipeline {
    agent any

     environment {
        
        registryCredential = 'ecr:us-east-2:awscreds'
        appRegistry = "public.ecr.aws/o5j9v9p7/devops"  

     }

    tools{
        maven "Maven"
    }
    
    stages{
              
        stage("Fetching"){
            steps{
                echo "Fetching the code"
                git branch: "cicd-docker", url: "https://github.com/testgit4me/cicd-jenkins.git"
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

        stage("Build docker image"){
            steps{
                script {                     
                    dockerImage = docker.build( appRegistry + ":$BUILD_NUMBER", ".")   
                }
            }
        } 

        stage('Upload App Image') {
          steps{
            script {
                docker.withRegistry("public.ecr.aws/o5j9v9p7", registryCredential) {
                        
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')  
                        
                    }                   
            }
          }
     }

    }  
}