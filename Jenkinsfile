pipeline 
{
  agent
  {
    docker { image 'maven:3.5.0-jdk-8' }
  }
  
  stages 
  {
    stage('Build') 
    {
      steps 
      {
		  withMaven(maven: 'Maven 3.5.0') 
		  {
		  	// Workaround for Jenkins issue 33510
			sh 'cd maven && mvn package -Dmaven.test.failure.ignore'
		  }
      }
    }
    
    stage('Document') 
    {
      steps 
      {
          withMaven(maven: 'Maven 3.5.0') 
          {
		  	// Workaround for Jenkins issue 33510
            sh 'cd maven && mvn site:site'
          }
      }
    }
    
    stage('Analyze') 
    {
      when
      {
      	expression {return currentBuild.result == "STABLE"}
      }
      steps 
      {
        echo 'Perform code analysis here.'
      }
    }
    
    stage('Deploy') 
    {
      steps 
      {
        echo 'Perform automated deployment here.'
      }
    }
    
    stage('Test') 
    {
      steps 
      {
        echo 'Perform automated functional tests here.'
      }
    }
  }
  
  post
  {
  	unstable
  	{
  		echo 'Unit tests failed.'
  	}
  }
}
