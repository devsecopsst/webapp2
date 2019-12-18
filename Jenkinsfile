pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Builds') {
      steps {
      sh 'mvn clean package'
      }
    }
    stage('deploy-tomcat'){
      steps{
        sshagent(['tomcat']){
        sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.133.145.106:/prod/apache-tomcat-8.5.50/webapps/webapp.war'
        }
      }
      
    }
  }
}
