pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  //environment {
   // ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  //}
   stages {
   stage('Building image') {
      steps{
          sh '''
        //  cd webapp
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker tag testapp 192.168.0.86:5000/mguazzardo/testapp
        docker push 192.168.0.86:5000/mguazzardo/testapp   
        '''
        }
      }
    }
}


    
  

