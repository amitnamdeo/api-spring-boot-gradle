pipeline {
    agent any
    stages {
        stage('status') {
            steps {
                // this is status step , can be removed
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
            post {
                always {
                    // to reports test result to show on jenkins
                    junit '**/build/*-results/test/TEST-*.xml'
                }
            }
        }
        stage('jacoco-report') {
            steps {
                publishHTML target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: false,
                        reportDir: 'build/reports/tests/test',
                        reportFiles: 'index.html',
                        reportName: 'JaCoCo Report',
                        reportTitles: ''
                    ]

            }
        }
        stage('sonar') {
            steps {
                 withSonarQubeEnv('sonar-qube-jenkins') {
                    sh './gradlew --info sonarqube'
                 }
            }
            post {
                always {
                    // wait in seconds for sonar process to complete
                    // for some reason waitForQualityGate was not working as expected
                    sleep 60
                }
            }
        }

        // No need to occupy a node
        stage("quality-check") {
            steps {
                 script {
                        timeout(time: 10, unit: 'MINUTES') { // Just in case something goes wrong, pipeline will be killed after a timeout
                            def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                            if (qg.status != 'OK') {
                                    error "Pipeline aborted due to quality gate failure: ${qg.status}"
                                }
                        }
                }
            }
            post {
                    success {
                          mail to:"Amit.Namdeo@footlocker.com", subject:"SUCCESS: ${currentBuild.fullDisplayName}", body: "Yay, we passed."
                    }
                    failure {
                          mail to:"Amit.Namdeo@footlocker.com", subject:"FAILURE: ${currentBuild.fullDisplayName}", body: "Boo, we failed."
                    }
            }
        }
        stage("Manual Input") {
            steps {
                sh 'echo " Manual steps"'
                input('OK to continue?')
            }    
        }
        stage("Post Manual") {
            steps {
                sh 'echo "  Post Manual"'
            }    
        }
    }
}