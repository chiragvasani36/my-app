node {    
	stage('Git CheckOut') 
	{    
		git url: 'https://github.com/chiragvasani36/my-app.git'
	}

	
	stage('Clean Old Packages') 
	{
		sh  'mvn clean'
	}
	stage('Maven Compile') 
	{
		sh  'mvn compile'
	}

	stage('Sonarqube analysis')
	{
		withSonarQubeEnv('sonar')
		{
			sh 'mvn sonar:sonar'
        }
	}
	
    stage("Quality Gate"){
          timeout(time: 10, unit: 'MINUTES') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
    }
    
	stage('Maven Package') 
	{
		sh  'mvn package'
	}
	}
