pipeline {
    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                  agent none
                    steps {
                        bat "run-tests.bat"
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
                stage('Test On Linux') {
                   agent none
                    steps {
                        bat "run-tests.bat"
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
            }
        }
    }
}