node(){

  stage('Git SCM Checkout'){
    git credentialsId: 'GitCredentials', url: 'https://github.com/abishek9114/webapp.git'
  }
  
  stage('Compile the package'){
    def mvnHome = tool name: 'maven-plugin', type: 'maven' 
    sh "${mvnHome)/bin/mvn package"

  }
  
}
