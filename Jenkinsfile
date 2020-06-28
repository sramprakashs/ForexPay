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


 
