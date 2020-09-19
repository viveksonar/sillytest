pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        echo 'Starting the pipeline'
        sh 'mvn clean'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn -Dtest=AlexaControllerTest test'
      }
    }

    stage('Deploy') {
      steps {
        archiveArtifacts 'target/*.war'
        sh 'AWS_ACCESS_KEY_ID=AKIA2WH2J45GHTLDH7D2 AWS_SECRET_ACCESS_KEY=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 aws s3 cp /var/lib/jenkins/workspace/sillyhacks2020_master/target/alexa-cicd-0.0.1-SNAPSHOT.war s3://elasticbeanstalk-ap-southeast-1-734964344652/2018362ew4-alexa-cicd-0.0.1-SNAPSHOT.war '
        sh 'AWS_ACCESS_KEY_ID=AKIA2WH2J45GHTLDH7D2 AWS_SECRET_ACCESS_KEY=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 AWS_DEFAULT_REGION=ap-southeast-1 aws elasticbeanstalk create-application-version --application-name Sillyhack2020 --version-label "kevin-jenkins$BUILD_DISPLAY_NAME" --description "Created by $BUILD_TAG"  --source-bundle=S3Bucket=elasticbeanstalk-ap-southeast-1-734964344652,S3Key=2018362ew4-alexa-cicd-0.0.1-SNAPSHOT.war'
        sh 'AWS_ACCESS_KEY_ID=AKIA2WH2J45GHTLDH7D2 AWS_SECRET_ACCESS_KEY=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 AWS_DEFAULT_REGION=ap-southeast-1 aws elasticbeanstalk update-environment --environment-name Sillyhack2020 --version-label "kevin-jenkins$BUILD_DISPLAY_NAME"'
        sh 'echo "$BUILD_URL"'
      }
    }

  }
}