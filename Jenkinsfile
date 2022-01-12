def CONNECT = 'http://192.168.56.103:8080'
def PROJECT = 'Webgoat8'
def STREAM = 'WebGoat8'

pipeline {
  
  agent any
  
  stages {
    stage("build") {
      steps {
        echo 'building the application...'
      }
    }
   stage("test") {
     steps {
       echo 'testing the application...'
     }
   }

   stage("BlackDuck Detect") {
      steps {
       script {
         synopsys_detect '--detect.tools=DETECTOR --detect.project.name=SPM-${JOB_NAME} --detect.project.version.name=${GIT_BRANCH} --detect.maven.path=/Users/dylanm/Build-Tools/apache-maven-3.8.3/bin/mvn'
      }
     }
   }
  }
 }

