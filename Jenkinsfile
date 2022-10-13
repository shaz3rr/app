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
                    echo "building jar"
                    gv.buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building image"
                    gv.buildImage()
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