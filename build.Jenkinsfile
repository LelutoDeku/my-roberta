pipeline {
    agent any

		environment {
			
			REGISTRY_URL = '060885648262.dkr.ecr.us-east-1.amazonaws.com'

		}
    stages {
        stage('Build') {
            steps {

					// sh 'ls'
					// sh 'echo building...'

					Retrieve DockerHub credentials by ID
					withCredentials([usernamePassword(credentialsId: 'Dockerhub', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {                    
					
					build the roberta image
					sh '''

					# Use docker login with your credentials
					docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}

					# build image
					docker build -t roberta:1.0-firstBuild .

					# tag image
					docker tag roberta:1.0-firstBuild hammad653/roberta:1.0-firstBuild

					#push image
					docker push ${DOCKERHUB_USERNAME}/roberta:1.0-firstBuild

					'''

					//or we use aws-ecr service
					// sh '''
					// aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $REGISTRY_URL					
					
					// # build image
					// docker build -t cicd-my-roberta .
					
					// # tag image
					// docker tag cicd-my-roberta:latest $REGISTRY_URL/cicd-my-roberta:latest					
					
					// #push image to ecr
					// docker push $REGISTRY_URL/cicd-my-roberta:latest
					// '''

				}
            }

			stage('Trigger Deploy') {
				    steps {
						        build job: 'my-roberta-cicd-deploy-pipeline' wait: false, parameters: [
									            string(name: 'ROBERTA_IMAGE_URL', value: "${DOCKERHUB_USERNAME}/roberta:1.0-firstBuild")
												]
					}
				}
        }
    }