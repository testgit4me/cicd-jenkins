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
                echo "Tesing the jar file"
                sh "mvn test"
            }
        }
        stage("Githook working"){
            steps{
                echo "Tesing githook"
                sh "mvn test"
            }
        }
    }

}