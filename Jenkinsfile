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
       stage('deploy to dev') {
                   agent none
                    steps {
                        echo "deploy to dev"
                    }
                    post {
                        always {
                            echo "deploy to dev result OK"
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
       stage('deploy to SIT') {
                   agent none
                    steps {
                        echo "deploy to SIT"
                    }
                    post {
                        always {
                            echo "deploy to SIT result OK"
                        }
                    }
                }

                      stage('Run Tests') {
            parallel {
                stage('security test SIT ') {
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
                stage('performance test SIT') {
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