pipeline {
  agent any
  stages {
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

  }
}