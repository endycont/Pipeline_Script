//import hudson.EnvVars
//import hudson.model.Environment
//def result2 = manager.build.result
pipeline {
	agent any
    tools {
        maven 'LocalMaven' 
        jdk 'LocalJDK8'
    }
    stages {
	    
        stage('job1'){
		agent {
			label "build"
		}
            steps {
                git 'https://github.com/endycont/Spring3MVC.git'
                bat label: '', script: 'mvn -B clean package'
                archiveArtifacts '**/*.war'
		echo "guardado war"
            }
        }
			
	stage('job3') {
				agent {
					label "deploy"
				}
				steps {
					echo"copia"
					 copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: '$JOB_NAME', selector: lastSuccessful()
           deploy adapters: [tomcat8(credentialsId: 'e75e8263-1318-412f-b78c-126095424d06', path: '', url: 'http://localhost:8081')], contextPath: null, war: '**/*.war'
				}
			}

	stage('job2'){
		agent {
			label "quality"
		}
            steps{
             git 'https://github.com/endycont/Spring3MVC.git'
             bat label: '', script: 'mvn -B checkstyle:checkstyle pmd:pmd'
             checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: '', unstableTotalAll: '1', unstableTotalHigh: '1', unstableTotalLow: '1', unstableTotalNormal: '1'
             pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
            
            } 
        }		

    }		
}

		






