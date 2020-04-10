pipeline {
   agent any

   stages {
      stage('checkout') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '794f1b08-837c-4548-8eca-07a0c0392f37', url: 'https://github.com/dthirumalaibe/cicd-buzz.git']]])
            python buzz/generator.py
         }
      }

   }
}
