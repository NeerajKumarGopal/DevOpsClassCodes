def readProb;
	def FAILED_STAGE
	pipeline {
	agent any
	tools {
        maven "mymaven"
        }
	stages {
	    stage('Setup') {
	    steps {
	        script {
	        readProb = readProperties  file:'testconfig.properties'
	        FAILED_STAGE=env.STAGE_NAME
	        Setup= "${readProb['Setup']}"
			if ("$Setup" == "yes") {
		 sh "git config --global user.email neer90k@gmail.com"
	        sh "git config --global user.name ${readProb['user.name']}"
	        sh 'git config --global credential.helper cache'
	        sh 'git config --global credential.helper cache'
	        sh "if [ -d ${readProb['Project_name']} ]; then rm -Rf ${readProb['Project_name']}; fi"
	        sh "if [ -d ${readProb['PMD_result']} ]; then rm -Rf ${readProb['PMD_result']};  fi"        
	        sh "mkdir ${readProb['PMD_result']}"
			}
			else {
			 echo "Skipped stage"
			}
			}
		}
		}
		}
		stage('Checkout') {
                    steps {
	                script {
		        git 'https://github.com/NeerajKumarGopal/DevOpsClassCodes.git'
	            }
		     dir('subDir') {
			   checkout "/tmp/${PACKAGE_NAME}_${BUILD_NUMBER}"
                    echo "Checkout is Completed"
                   }
               }
           }
		stage('Build') {
			steps {
				script {
					sh "mvn -version"
					sh "mvn clean test"
	                                sh "mvn compile"
					echo "Maven Compile Stage is completed"
				}
			}
		}
	}
