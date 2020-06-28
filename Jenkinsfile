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

 

 

 

    
 

  } 

 

 

}


 
