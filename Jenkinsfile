pipeline {
  agent any
  stages {
    stage('Compile (build) ') {
      parallel {
        stage('Compile (build) ') {
          steps {
            sh '''#!/bin/bash
echo "*******-Starting CI CD Pipeline Tasks-*******"
#-BUILD
echo ""
echo "..... Build Phase Started :: Compiling Source Code :: ......"
cd java_web_code
mvn install'''
          }
        }

        stage('BUILD (TEST)') {
          steps {
            sh '''#!/bin/bash


#-BUILD (TEST)
echo ""
echo "..... Test Phase Started :: Testing via Automated Scripts :: ......"
cd ../integration-testing/
mvn clean verify -P integration-test'''
          }
        }

      }
    }

    stage('POSTBUILD') {
      steps {
        sh '''#!/bin/bash
#-POSTBUILD (PROVISIONING DEPLOYMENT)
echo ""
echo "..... Integration Phase Started :: Copying Artifacts :: ......"
cd java_web_code/
/bin/cp target/wildfly-spring-boot-sample-1.0.0.war ../docker/
echo ""
echo "..... Provisioning Phase Started :: Building Docker Container :: ......"
cd ../docker/
sudo docker build -t devops_pipeline_demo .
'''
      }
    }

    stage('deployment phase') {
      steps {
        sh '''docker run -d -p 8180:8080 --name devops_pipeline_demo devops_pipeline_demo


#-Completion
echo "--------------------------------------------------------"
echo "View App deployed here: http://server-ip:8180/sample.txt"
echo "--------------------------------------------------------"'''
      }
    }

  }
}