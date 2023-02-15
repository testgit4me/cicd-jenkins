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
        
        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }

       
    }
    
}