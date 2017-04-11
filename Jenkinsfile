node {
    
   def maven = tool 'MAVEN'
    
   stage('Build') {
        git url: 'https://github.com/checholin87/time-tracker.git', branch: 'master'
        sh "'${maven}/bin/mvn' clean install -Dmaven.test.failure.ignore=true"
        archive 'web/target/*.war'
        archive 'core/target/*.jar'
        sh 'cd core/target/surefire-reports/ && touch *.xml'
        junit 'core/target/surefire-reports/TEST-*.xml'
        sh "cd core && '${maven}/bin/mvn' org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar -Dsonar.host.url=\"http://192.168.99.100:9000\""
   }

   stage('Deploy QA') {
       sh "curl -u admin:password -X PUT 'http://192.168.99.100:8081/artifactory/ext-snapshot-local/training/time-tracker/time-tracker-web/0.3.1-SNAPSHOT/time-tracker-web-0.3.1-SNAPSHOT.war' -T 'web/target/time-tracker-web-0.3.1-SNAPSHOT.war'"
       sh "curl -u admin:tomcat --upload-file 'web/target/time-tracker-web-0.3.1-SNAPSHOT.war' 'http://192.168.99.100:8888/manager/text/deploy?path=/time-tracker-web&update=true'"
   }
   
   stage('Functional Test') {
   }
   
   stage('Release') {
   }
}
