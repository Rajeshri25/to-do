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


     stage ('Push K8S manifest SCM'){
      steps{
       git credentialsId: '7c571f02-5769-47b5-aca3-31a8f39dbaf4', url: 'https://github.com/Rajeshri25/new-repo.git'
        branch: 'main'
      }
     }
    

       stage ('Updates K8s manifest & push to Repo'){
      steps{
        scripts{
       withCredentials([string(credentialsId: '9e2a7009-ebb0-4aa5-b08f-38ea7421b7c6', variable: 'welcome')]) {
        sh '''cat deploy.yaml
 sed -i \'\' "s/32/${BUILD_NUMBER}/g" deploy.yaml
cat deploy.yaml
git add deploy.yaml
git commit -m \'Updated the deploy yaml | Jenkins Pipeline\'
git remote -v
git push https://github.com/Rajeshri25/new-repo.git HEAD:main''' 
    }

    
      
    
  }
}
