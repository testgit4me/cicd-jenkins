#!/usr/bin/env groovy

Pipeline{
    agent any
    maven "Maven"
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

    }

}