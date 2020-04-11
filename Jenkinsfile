pipeline {
   agent any

   stages {
      stage('checkout_Code_integration') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '794f1b08-837c-4548-8eca-07a0c0392f37', url: 'https://github.com/dthirumalaibe/cicd-buzz.git']]])
            
         }
      }
      stage('Unit_Testing') {
         steps {
			sh "/usr/local/bin/pip install -r requirements.txt"
            sh "/bin/python3 -m pytest -v tests/test_generator.py"
         }
      }
      stage('Docker_image_Build') {
         steps {

            sh "/bin/docker build -t dthirumalaibe/cicd-buzz:latest ."
            
         }
      }
      stage('publish') {
         steps {
            
            withDockerRegistry(credentialsId: '794f1b08-837c-4548-8eca-07a0c0392f37', url: 'https://index.docker.io/v1/') {

			sh "docker push dthirumalaibe/cicd-buzz:latest"
         }
         }
      }
      stage('Running_image_from_DockerHub') {
         steps {
            
           sh "/bin/docker run -p 5000:5000 --rm dthirumalaibe/cicd-buzz:latest"
         }
         }
      }
   }

