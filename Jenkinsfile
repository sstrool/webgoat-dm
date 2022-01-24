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
   stage('Coverity Full Scan') {
     steps {
       withCoverityEnvironment(coverityInstanceUrl: "$CONNECT", projectName: "$PROJECT", streamName: "$STREAM") {
            sh '''
                cov-build --dir idir /Users/dylanm/Build-Tools/apache-maven-3.8.3/bin/mvn -B clean package -DskipTests
                cov-analyze --dir idir --strip-path $WORKSPACE --webapp-security
                cov-commit-defects --dir idir --url $COV_URL --stream $COV_STREAM --scm git
            '''
        }
      }
    }
   stage("BlackDuck Detect") {
      steps {
       script {
         synopsys_detect '--detect.tools=DETECTOR,BINARY_SCAN --detect.project.name=SPM-${JOB_NAME} --detect.project.version.name=${GIT_BRANCH} --detect.maven.path=/Users/dylanm/Build-Tools/apache-maven-3.8.3/bin/mvn --detect.binary.scan.file.path=/Users/dylanm/Projects/webgoat/webgoat-server/target/webgoat-server-8.2.1-SNAPSHOT.jar'
        }
      }
    }
  }
}

