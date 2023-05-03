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
                dir('dockdemo2') {
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
                dir('sampleDockProj1') {
                  sh '''
                  docker build . -t nandhinitk/sampledockproj2
                  '''
                }
            }
        }

        stage("Push image to Docker hub") {
            steps {
                sh '''
                docker login -u nandhinitk -p Kalakrish@13
                docker push nandhinitk/sampledockproj1
                docker push nandhinitk/sampledockproj2
                '''
            }
        }

        stage("Run apps") {
            steps {
                sh '''
                docker run -p 8001:8001 nandhinitk/sampledockproj1
                docker run -p 8002:8002 nandhinitk/sampledockproj2
                '''
            }
        }
    }
}