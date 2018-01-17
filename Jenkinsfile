pipeline {
    agent any
    stages {
        stage('status') {
            steps {
                sh 'echo " --- --- --- --- --- --- --- --- --- --- "'
                sh './gradlew properties'
                sh 'echo " --- --- --- --- --- --- --- --- --- --- "'
            }
        }
        stage('clean') {
            steps {
                sh './gradlew clean'
            }
        }
        stage('build') {
            steps {
                 script {
                            try {
                                sh './gradlew build'
                            }
                            catch (Exception e)
                            {
                                // for jenkin server https://azu-jenkins01:8443/job/gradle-pipe-demo/
                                withEnv(['JAVA_HOME=/var/lib/jenkins/tools/hudson.model.JDK/Java8'])
                                    {
                                        sh 'echo " --- c --- a --- t --- c --- h --- --- b --- l --- o --- c --- k --- "'
                                        sh './gradlew build'
                                    }
                            }
                    }
            }
        }
    }
}