#!/usr/bin/env groovy

pipeline {
    agent any

     environment {
        registryCredential = 'ecr:us-east-2:awscreds'
        appRegistry = "projectvprofile/dockercicd"        
        vprofileRegistry = "public.ecr.aws/o5j9v9p7"
        // appRegistry = "753743851231.dkr.ecr.us-east-2.amazonaws.com/jenkinscicd"        
        // vprofileRegistry = "753743851231.dkr.ecr.us-east-2.amazonaws.com"
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
                    docker.withRegistry('dockerHub-login') {

                        def dockerImage = docker.build( appRegistry + ":$BUILD_NUMBER", ".")    
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')  
                        
                    }             
                }
            }
        } 

    }  
}