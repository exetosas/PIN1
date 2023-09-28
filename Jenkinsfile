pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
   // ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"

    NEXUS_USUARIO="admin"
    NEXUS_CONTRASENA="admin"
    NEXUS_URL="192.168.0.86:8083"
    NEXUS_URL_PUSH="192.168.0.86:8083"

  }
   stages {
   stage('Building image') {
      steps{
          sh '''
        
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh '''
        docker run testapp npm test
        '''
      }
    }
   /*docker login -u $NEXUS_USUARIO -p $NEXUS_CONTRASENA  $NEXUS_URL*/
   /*
      docker tag testapp 127.0.0.1:5000/mguazzardo/testapp
      docker push 127.0.0.1:5000/mguazzardo/testapp
   */
   stage('Deploy Image') {
      steps{
        sh '''
          docker run --rm -d -p 5000:5000 --name dockerregistry registry:latest
          docker tag testapp 127.0.0.1:5000/mguazzardo/testapp
          docker push 127.0.0.1:5000/mguazzardo/testappdocker
          docker stop dockerregistry
        '''
        }
      }
    }
}


    
  

