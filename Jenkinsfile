pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
   // ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"

    NEXUS_USUARIO="admin"
    NEXUS_CONTRASENA="admin"
    NEXUS_URL="192.168.0.86:8081"
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
   stage('Deploy Image') {
      steps{
        sh '''
        
        docker tag mirepo $NEXUS_URL_PUSH/mguazzardo/testapp
        docker push $NEXUS_URL_PUSH/mguazzardo/testapp   
        '''
        }
      }
    }
}


    
  

