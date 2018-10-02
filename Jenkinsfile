pipeline {
  triggers{ cron("H 10 * * *") }
  agent {
    docker {
      image 'maven:3.5.2-jdk-8'
    }
  }
  stages {
    stage('Build') {
          steps {
            sh 'mvn clean test'
            cucumber 'target/cucumber.json'
          }
       }
  }
  post{
    failure {
         echo "Test failed"
         mail(bcc: '',
            body: "Run ${JOB_NAME}-#${BUILD_NUMBER} failed.\n\
            To get more details, visit the build results page:\
            ${BUILD_URL}/cucumber-html-reports/overview-features.html.",
            cc: '',
            from: 'amp-dev@ebi.ac.uk',
            replyTo: '',
            subject: "${JOB_NAME} ${BUILD_NUMBER} failed",
            to: 'amp-dev@ebi.ac.uk')
     }
  }
}
