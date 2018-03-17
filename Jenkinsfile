pipeline {

  /*
   * Run everything on an existing agent configured with a label 'docker'.
   * This agent will need docker, git and a jdk installed at a minimum.
   */
agent any 

  // using the Timestamper plugin we can add timestamps to the console log
  options {
    timestamps()
  }

  stages {
    stage('Build') {
   echo 'Build here...'
      }
      steps {
        // using the Pipeline Maven plugin we can set maven configuration settings, publish test results, and annotate the Jenkins console
        withMaven(options: [findbugsPublisher(), junitPublisher(ignoreAttachments: false)]) {
          bat 'dir'
        }
      }
      post {
        success {
          // we only worry about archiving the jar file if the build steps are successful
         // archiveArtifacts(artifacts: '**/target/*.jar', allowEmptyArchive: true)
         echo 'archive artifact here...'
        }
      }
    

    stage('Quality Analysis') {
      parallel {
        // run Sonar Scan and Integration tests in parallel. This syntax requires Declarative Pipeline 1.2 or higher
        stage ('Integration Test') {
          agent any  //run this stage on any available agent
          steps {
            echo 'Run integration tests here...'
          }
        }
        stage('Sonar Scan') {
           agent any 
              // we can use the same image and workspace as we did previously

          steps {
           echo 'Run sonar  here...'
          }
        }
      }
    }

    stage('Build and Publish Image') {
      when {
        branch 'master'  //only run these steps on the master branch
      }
      steps {
        /*
         * Multiline strings can be used for larger scripts. It is also possible to put scripts in your shared library
         * and load them with 'libaryResource'
         */
        bat """
          docker ps .
          docker ps 
          docker ps
        """
      }
    }
  }
}
  post {
    failure {
      // notify users when the Pipeline fails
      mail to: 'team@example.com',
          subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
          body: "Something is wrong with ${env.BUILD_URL}"
    }
  }
