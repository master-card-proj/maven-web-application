pipeline{
  agent any
  tools{
    maven "maven3.8.7"
  }
  stages{
    stage('clone'){
      steps{
        git 'https://github.com/master-card-proj/maven-web-application.git'
      }
    }
    stage('test&build'){
      steps{
        sh "mvn clean package"
      }
    }
    stage(codequality){
      steps{
        sh "mvn sonar:sonar"
      }
    }
     stage(uploadtoNexus){
      steps{
        sh "mvn deploy"
      }
    }
    stage(deploytoProd){
      steps{
             deploy adapters: [tomcat8(credentialsId: 'tomcatcred', path: '', url: 'http://52.15.37.167:8080/')], contextPath: null, war: 'target/*war'
            }
        }
  }
}
