#!groovy

node('node') {


    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

            stage 'Checkout'

       }

 stage('Sonarqube Static Analysis') {
print "Sonarqube running"
        bat "./dir"

 }

       stage('Test'){

         env.NODE_ENV = "test"

         print "Environment will be : ${env.NODE_ENV}"

         bat 'node -v'
         bat 'npm prune'
         bat 'npm install'
         bat 'npm test'

       }

       stage('Build Docker'){

            bat 'docker ps'
       }

       stage('Deploy'){

         echo 'Push to Repo'
        bat 'docker ps'

         echo 'ssh to web server and tell it to pull new image'
       bat 'docker ps'

       }

       stage('Cleanup'){

         echo 'prune and cleanup'
         bat 'npm prune'
         bat 'rm node_modules -rf'

         mail body: 'project build successful',
                     from: 'xxxx@yyyyy.com',
                     replyTo: 'xxxx@yyyy.com',
                     subject: 'project build successful',
                     to: 'yyyyy@yyyy.com'
       }



    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'xxxx@yyyy.com',
            replyTo: 'yyyy@yyyy.com',
            subject: 'project build failed',
            to: 'zzzz@yyyyy.com'

        throw err
    }
