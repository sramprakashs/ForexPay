pipeline { 
   agent any 
stages { 
             stage('Git Checkout') { 
                steps { 
                     git 'https://github.com/samridhi97/ForexPay.git' 

}} 
   stage('Build') { 
steps { 
withSonarQubeEnv('sonar') { 
sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true' 
}}} 
     stage("Quality Gate") { 

 

                steps { 

 

                    timeout(time: 1, unit: 'MINUTES') { 

 

                    waitForQualityGate abortPipeline: true 

 

              }}} 

 

 

 

    stage ('Deploy') { 

 

steps { 

 

sh '/opt/maven/bin/mvn clean deploy -Dmaven.test.skip=true' 

 

}} 

 

 

 

    stage ('Release') { 

 

steps { 

 

sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &' 

 

}} 

 

 

 

   stage ('DB Migration') { 

 

steps { 

 

sh '/opt/maven/bin/mvn clean flyway:undo' 

 

}}
stage( 'email' ){

            steps{

               emailext body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
 
              <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""", subject: "The Application has been deployed. Job: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", to: 'samridhii.bareja9719@gmail.com'
            }

        }} 

 

 

}


 
