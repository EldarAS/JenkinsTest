pipeline {
 agent none
 stages {

 stage('0. Initialize') {
  agent any
  steps {
   echo "Init -clean"
    bat "mvn -version"
  }
  post {
   always {
    echo "Initialize result OK"
   }
  }
 }


 stage('1. Build and check code') {
  parallel {
   stage('1a. Build') {
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

   stage('1b. Unit test') {
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

   stage('1c. sonarqube') {
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

 stage('2. Add to nexus artifact repo') {
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

 stage('3. deploy to dev') {
  parallel {
   stage('3a. Security test cloudformation scripts') {
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

   stage('3b. deploy dev') {
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
 stage('4. Run Tests dev') {
  parallel {
   stage('4a. deployment test') {
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
   stage('4b. endpoint test') {
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



 stage('5. deploy to SIT') {
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


 stage('6. Run initial Tests SIT') {
  parallel {
   stage('6a. deployment test') {
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
   stage('6b endpoint test') {
    agent any
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
 stage('7. Run Tests SIT') {
  parallel {
   stage('7a. security test SIT ') {
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
   stage('7b performance test SIT') {
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
  stage('Manual verfication deploy to UAT') {
  agent none
  steps {
   input id: 'Deploy', message: 'Proceed with UAT deployment?', ok: 'Deploy!'
  }
  post {
   always {
    echo "deploy to UAT result OK"
   }
  }
 }
 stage('8. Run initial Tests UAT') {
  parallel {
   stage('8a. deployment test') {
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
   stage('8b endpoint test') {
    agent any
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
 stage('10. Run Tests UAT') {
  parallel {
   stage('10a. security test UAT ') {
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
   stage('10b performance test UAT') {
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
  stage('Manual verfication deploy to Prod') {
  agent none
  steps {
   input id: 'Deploy', message: 'Proceed with Prod deployment?', ok: 'Deploy!'
  }
  post {
   always {
    echo "deploy to Prod result OK"
   }
  }
 }
 stage('11. Run initial Tests Prod') {
  parallel {
   stage('11a. deployment test') {
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
   stage('11b endpoint test') {
    agent any
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
 stage('12. Run Tests Prod') {
  parallel {
   stage('12a. security test Prod ') {
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
   stage('12b blue/green') {
    agent none
    steps {
     echo "test deploy"
    }
    post {
     always {
      echo "test deploy OK"
     }
    }
   }
  }
 }

}
}