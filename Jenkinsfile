pipeline{
  agent any
  environment {
    IMAGE_TAG = "${BUILD_NUMBER}"
  }
  stages{
    
    stage ('Checkout'){
      steps{
        git credentialsId: '7c571f02-5769-47b5-aca3-31a8f39dbaf4', url: 'https://github.com/Rajeshri25/to-do.git'
        branch: 'main'
      }
    }

     stage ('Biuld Docker'){
      steps{
        sh '''
        echo Build docker image
        docker build -t rajeshri/cicd-pipe:${BUILD_NUMBER} .
        '''
     
      }
    }


     stage ('Push the artifacts'){
      steps{
        sh '''
        echo Push to Repo
        docker push rajeshri/cicd-pipe:${BUILD_NUMBER}
        '''
        
      }
    }


     stage ('Checkout'){
      steps{
        git credentialsId: '7c571f02-5769-47b5-aca3-31a8f39dbaf4', url: 'https://github.com/Rajeshri25/to-do.git'
        branch: 'main'
      }
    }

    
      
    
  }
}
