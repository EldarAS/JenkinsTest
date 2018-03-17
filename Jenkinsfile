pipeline {
    agent none
    stages {
  stage('build') {
                   agent none
                    steps {
                        echo "build"
                    }
                    post {
                        always {
                            echo "build result"
                        }
                    }
                }
  stage('sonarqube') {
                   agent none
                    steps {
                        echo "sonarqube"
                    }
                    post {
                        always {
                            echo "sonar qube result"
                        }
                    }
                }
        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                  agent none
                    steps {
                        echo "test windows"
                    }
                    post {
                        always {
                            echo "test windows result"
                        }
                    }
                }
                stage('Test On Linux') {
                   agent none
                    steps {
                          echo "test Linux"
                    }
                    post {
                        always {
                           echo "test linux result"
                        }
                    }
                }
            }
        }
    }
}