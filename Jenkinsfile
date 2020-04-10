pipeline {
   agent any

   stages {
      stage('checkout') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '794f1b08-837c-4548-8eca-07a0c0392f37', url: 'https://github.com/dthirumalaibe/cicd-buzz.git']]])
            
         }
      }
      stage('Check_py_code') {
         steps {
            sh "/bin/python3 buzz/generator.py"
         }
      }
      stage('Build_Docker_image') {
         steps {

            sh "/bin/docker build -t dthirumalaibe/cicd-buzz:1.0 ."
            //sh "/bin/docker run -p 5000:5000 --rm cicd-buzz"
         }
      }
      stage('publish_to_DockerHub') {
         steps {
            
            withDockerRegistry(credentialsId: '794f1b08-837c-4548-8eca-07a0c0392f37', url: 'https://index.docker.io/v1/') {

			sh "docker push dthirumalaibe/cicd-buzz:1.0"
         }
         }
      }
   }
}

