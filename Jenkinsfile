#!/usr/bin/env groovy

@Library ('jenkins-shared-library')
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
            when {
                expression {
                   BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build image") {
            when {
                expression {
                   BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    buildImage()
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