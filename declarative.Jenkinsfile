pipeline {
    agent any
    stages {
        stage('status') {
            steps {
                sh 'echo "Hello World"'
                sh './gradlew properties'
            }
        }
        stage('clean') {
            steps {
                sh './gradlew clean'
            }
        }
        stage('build') {
            steps {
                sh './gradlew build'
                // OR sh ./gradlew compileJava compileTestJava  jar
            }
        }
    }
}


// ./gradlew properties

// ./gradlew clean


// ./gradlew test  jar

// ./gradlew build   [COMPILE+TEST+JAR]
// TO RUN ->   java -jar build/libs/api-spring-boot-gradle-0.1.0.jar  OR  gradle bootRun
