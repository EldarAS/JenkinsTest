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
 stage('Add to nexus artifact repo') {
                   agent none
                    steps {
                        echo "Add to nexus artifact repo"
                    }
                    post {
                        always {
                            echo "Add to nexus artifact repo OK"
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
        stage('Run Tests dev') {
            parallel {
                stage('deployment test') {
                  agent none
                    steps {
                        echo "test deployment"
                    }
                    post {
                        always {
                            echo "test deployment result OK"
                        }
                    }
                }
                stage('endpoint test') {
                   agent none
                    steps {
                          echo "test endpoint"
                    }
                    post {
                        always {
                           echo "test endpoint result OK"
                        }
                    }
                }
            }
        }
  stage('Deploy SIT approval'){
    input "Deploy to SIT?"
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

                      stage('Run Tests SIT') {
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