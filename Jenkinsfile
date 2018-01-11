pipeline {
    agent any
    stages {

        stage('Test') {
            steps {
                sh 'echo "Test"'

            }
        },

        stage('Build') {
                    steps {
                        sh 'echo "Hello World"'
                        sh '''
                            echo "Multiline shell steps works too"
                            ls -lah
                        '''
                    }
                }
    }
}
