pipeline {
    agent any

    environment {
	DOCKER_TAG = getVersion()
     }

  stages {
    stage ('Clone Stage') {
      steps {
	git branch: 'main', url: 'https://github.com/ChalloufNour/devops_project.git'
	}
    }

      stage('Build Backend Image') {
            steps {
                dir('spring-boot-server') {
                    script {
                        sh 'docker build -t nour001/backend:${DOCKER_TAG} .'
                    }
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('angular-14-client') {
                    script {
                        sh 'docker build -t nour001/frontend:${DOCKER_TAG} .'
                    }
                }
            }
        }
     
     stage ('DockerHub Push') {
	steps {
		withCredentials([string(credentialsId: 'mydockerhubpassword', variable:
	'DockerHubPassword')]) {
	sh 'docker login -u nour001 -p ${DockerHubPassword}'
	}
	sh 'docker push nour001/backend:${DOCKER_TAG}'
	sh 'docker push nour001/frontend:${DOCKER_TAG}'
	}
     }
     
    

   }
}

def getVersion(){
def version = sh returnStdout: true, script: 'git rev-parse --short HEAD'
return version
}



