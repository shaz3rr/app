#!/usr/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
        remote: 'https://github.com/shaz3rr/JenkinsSL.git',
        credentialsId: 'dockerhub'
        ]
)
//@Library('jenkins-shared-library@master')


def gv

pipeline {
    agent any

    tools {
        maven 'maven-3.8'
    }

    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    buildImage 'localhost:8083/java-maven-app:4.0'
                    dockerLogin()
                    dockerPush 'localhost:8083/java-maven-app:4.0'
                }
            }
        }
        stage("deploy") {
            input {
                message "Select the environment to deploy"
                ok "Done"
                parameters {
                    choice(name: 'ENV', choices: ['production', 'staging', 'development'], description: 'env type')

                }
            }
            steps {
                script {
                    echo "Deploying ${ENV}"
                    //gv.deployApp()
                }
            }
        }
    }
}