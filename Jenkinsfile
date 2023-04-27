pipeline {
    agent any

    stages {
        stage("Build") {
            steps {
                gradlew clean build
            }
        }
    }
}