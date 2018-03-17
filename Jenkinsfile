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
                            echo "sonar qube result OK"
                        }
                    }
                }
        stage('Run Tests') {
            parallel {
                stage('security test') {
                  agent none
                    steps {
                        echo "test security"
                    }
                    post {
                        always {
                            echo "test security result OK"
                        }
                    }
                }
                stage('performance test') {
                   agent none
                    steps {
                          echo "test performance"
                    }
                    post {
                        always {
                           echo "test performance result OK"
                        }
                    }
                }
            }
        }
    }
}