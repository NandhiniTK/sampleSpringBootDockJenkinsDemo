pipeline {
    agent any

    tools {
        gradle '7.6.1'
    }

    stages {
        stage("Build") {
            steps {
                echo "Build stage"
                echo "Workspace is ${WORKSPACE}"
                dir('sampleDockProj1') {
                  sh '''
                  gradle clean
                  gradle build
                  '''
                }
             }
        }

        stage("Build docker image") {
            steps {
                echo "Build Docker images stage"
                dir('sampleDockProj1') {
                  sh '''
                  docker build . -t nandhinitk/sampledockproj1
                  '''
                }
            }
        }

        stage("Push image to Docker hub") {
            steps {
                sh '''
                docker login -u nandhinitk -p Kalakrish@13
                docker push nandhinitk/sampledockproj1
                '''
            }
        }

        stage("Push image to Docker hub") {
            steps {
                sh '''
                docker run -p 8001:8080 nandhinitk/sampledockproj1
                '''
            }
        }
    }
}