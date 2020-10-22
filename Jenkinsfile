node ('mster')
 {
  
  def mavenHome = tool name: "maven3.6.3"
  
      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"
  
    stage('checkoutcode')
    {
    git credentialsId: 'e6f7d7c7-17c7-4c8d-86a8-113eeddf83bf', url: 'https://github.com/srinivasa1122/maven-web-application.git'
    }
    stage('build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('sonarqubereport')
    {
         sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('uploadartifacts into nexus')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('deployappintoTomcat')
    {
      sshagent(['b93b0e4b-3aab-438b-bef8-036feb9590aa']) 
      {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.224.74:/opt/apache-tomcat-9.0.39/webapps/"
      }
 
    }
    stage('sendmail notification')
    {
        emailext body: '''srinivasa y v
software solutions....
buil over...''', subject: 'Build over!!!', to: 'srinivasayv1122@gmail.com'
    }

}
