pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // sh 'ls'
                // sh 'echo building...'

				// Retrieve DockerHub credentials by ID
                withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {                    
                
				// Log in to DockerHub
				sh '''

                # Use docker login with your credentials
                docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}

				# build image
				docker build -t roberta:1.0-firstBuild .

				# tag image
				docker tag roberta:1.0-firstBuild first-roberta

				#push image
				docker push ${DOCKERHUB_USERNAME} roberta:1.0-firstBuild

				'''

				}
            }
        }
    }
}