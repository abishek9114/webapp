node(){

  stage('Git SCM Checkout'){
    git credentialsId: 'GitCredentials', url: 'https://github.com/abishek9114/webapp.git'
  }
  
  stage('Complie-Package'){
    def mvnHome = tool name: 'maven-plugin', type: 'maven'
    sh "${mvnHome}/bin/mvn clean package"
  }
  
  stage('Send Over Ansible'){
    sshPublisher(publishers: [sshPublisherDesc(configName: 'ansibleserver', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''ansible-playbook -i /opt/docker/ansible-host /opt/docker/devops.yml;
      ansible-playbook -i /opt/docker/ansible-host /opt/docker/push-devops.yml;''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt/docker/', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
  
  }
  stage('Slack-Notification'){
        slackSend baseUrl: 'https://hooks.slack.com/services/', 
        channel: '#jenkins-pipeline-practice', 
        color: 'good', 
        message: 'Job Creation Status', 
        tokenCredentialId: 'slack-demo'
        
        }
}
