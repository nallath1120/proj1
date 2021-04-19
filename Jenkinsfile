pipeline { 

environment { 

	registry = "ntr1/sample" 

	registryCredential = 'dockerhub1.1' 

	dockerImage = '' 

}

agent any 

stages { 

	stage('Cloning our Git') { 

		steps { 

			git 'https://github.com/nallath1120/proj1.git' 

		}

	} 

	stage('Building our image') { 

		steps { 

			script { 

				dockerImage = docker.build registry + ":$BUILD_NUMBER" 

			}

		} 

	}

	stage('Push our image') { 
		steps { 

			script { 

				docker.withRegistry( '', registryCredential ) { 

					dockerImage.push() 

				}

			} 

		}

	} 


    stage ('Deploy to Conatiner') {
     steps {
         echo "Run containers" + dockerImage
         script {
          sh "docker run -d -p 8081:80 $registry:$BUILD_NUMBER"
                     }
                  }
  } 
  
/*
	stage('Cleaning up') { 

		steps { 

			sh "docker rmi $registry:$BUILD_NUMBER" 

		}

	} 
*/

}

}
