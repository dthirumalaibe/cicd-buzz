pipeline {
   agent any

   stages {
      stage('checkout') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '794f1b08-837c-4548-8eca-07a0c0392f37', url: 'https://github.com/dthirumalaibe/cicd-buzz.git']]])
            
         }
      }
      stage('run') {
         steps {
            sh "/bin/python3 buzz/generator.py"
         }
      }
      stage('Test') {
         steps {

            sh "/bin/docker build -t cicd-buzz ."
            sh "/bin/docker run -p 5000:5000 --rm cicd-buzz"
         }
      }
   }
}

