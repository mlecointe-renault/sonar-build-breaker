node ('master') {
          
	 stage('Preparation') { // for display purposes
      // Cleaning workspace
      cleanWs()
      
   }
	
          stage('Checkout') {
	    checkout scm
	}
          
         stage ('Build') {
           
                sh 'mvn -U clean package  ' 
            
        }
	
	 stage('Code Quality') {
             
                echo 'Checking Code Quality'
                withSonarQubeEnv('ASF Sonar Analysis') {
                    sh 'mvn   sonar:sonar'
                }
           }
	stage("Quality Gate") {
    		timeout(time: 1, unit: 'HOURS') {
        		def qg = waitForQualityGate()
        		if (qg.status != 'OK') {
           			 error "Pipeline aborted due to quality gate failure: ${qg.status}"
        		}
    		}
	}
		 
 
}
