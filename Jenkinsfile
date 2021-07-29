node('slaves'){
    def mavenhome = tool name:"maven3.6.3"
    stage('checkout'){
        git branch: 'development', credentialsId: '8c254bb9-1859-4bee-addc-ff7181206f0c', url: 'https://github.com/kotipisandeep/maven-web-application.git'
    }
stage('build'){
    sh "${mavenhome}/bin/mvn clean package"
}
    
 
stage('execuutesonar qube  report'){
    sh "${mavenhome}/bin/mvn clean sonar:sonar"
}
stage('uploadartifact into nexus'){
    sh "${mavenhome}/bin/mvn deploy"
}
stage('deploy tomcat server')
{
    sshagent(['f4351532-9b07-4c77-a6d1-77ba573320bf']) {
   sh "scp  -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.45.211:/opt/apache-tomcat-9.0.50/webapps"

}
}
stage('send email notification')
{
    emailext body: 'regards pora puka,kojja', subject: 'build over..', to: 'chandramohan870915@gmail.com,sandeep8008700138@gmail.com'
}
}
