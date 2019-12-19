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
    stage('Deploy-To-Tomcat'){
      steps{
        sshagent(['tomcat']){
        sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@52.14.50.132:/prod/apache-tomcat-8.5.50/webapps/webapp.war'
        }
      }
      
    }
  }
}
