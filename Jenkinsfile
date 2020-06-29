pipeline { 
   agent any 
stages { 
             stage('Git Checkout') { 
                steps { 
                     git 'https://github.com/samridhi97/ForexPay.git' 

}} 
   stage('Build') { 
steps { 

sh '/opt/maven/bin/mvn clean verify -Dmaven.test.skip=true' 
}}
   stage('Please Provide Approval for SIT Deployment ?'){

steps{

slackSend baseUrl: 'https://hooks.slack.com/services/', channel: 'jenkins', color: 'bad', message: "${env.BUILD_URL}", tokenCredentialId: 'slack', username: 'samridhi bareja'

script{

def userInput

try {

userInput = input(

id: 'Proceed1', message: 'SIT Deployment Approval', parameters: [

[$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please Confirm you agree with this']

])

} catch(err) {

def user = err.getCauses()[0].getUser()

userInput = false

echo "Aborted by: [${user}]"

}

}

}

}
    
 

 

 

    stage ('Deploy') { 

 

steps { 

 

sh '/opt/maven/bin/mvn clean deploy -Dmaven.test.skip=true' 

 

}} 

 stage('Deployment-SIT'){
      steps{
        sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''PATH=$PATH:/usr/bin export PATH
ansible-playbook forexp.yml''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
      }
   }

 

 

    
 

  } 

 

 

}


 
