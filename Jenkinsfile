pipeline {
 agent none
 stages {

 stage('Initialize') {
  agent any
  steps {
   echo "Init -clean"
    bat "mvn -version"
  }
  post {
   always {
    echo "Initialize result"
   }
  }
 }

 stage('Build and check code') {
  parallel {
   stage('Build') {
 //agent { docker 'openjdk:8-jdk-alpine'}
 agent any
    steps {
  //echo "build"
  //sh "mvn -version"   
    bat "mvn -version"
    }
    post {
     always {
      echo "build result"
     }
    }
   }

   stage('Unit test') {
    agent none
    steps {
     echo "Unit test"
    }
    post {
     always {
      echo "Unit test result"
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
      echo "sonarqube result OK"
     }
    }
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
  parallel {
   stage('Security test cloudformation scripts') {
    agent none
    steps {

     echo "CFN_NAG run"
    }
    post {
     always {
      echo "CFN_NAG run OK"
     }
    }
   }

   stage('deploy dev') {
    agent any
    steps {
     echo "deploy"
       //powershell "aws s3 ls"
    }
    post {
     always {
      echo "deploy to dev result OK"
     }
    }
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

 stage('Manual verfication deploy to SIT?') {
  agent none
  steps {
   input id: 'Deploy', message: 'Proceed with SIT deployment?', ok: 'Deploy!'
  }
  post {
   always {
    echo "deploy to SIT result OK"
   }
  }
 }

 stage('deploy to SIT') {
  agent none
     when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' (1)
              }
            }
  steps {
   echo "deploy to SIT"
  }
  post {
   always {
    echo "deploy to SIT result OK"
   }
  }
 }


 stage('Run initial Tests SIT') {
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
    agent any
    steps {
     echo "test endpoint"
     powershell(returnStdout: true, script: '''
       cd c:/Dev/Postman/
       newman run test.postman_collection.json
    ''')
   
    }
    post {
     always {
      echo "test endpoint result OK"
     }
    }
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