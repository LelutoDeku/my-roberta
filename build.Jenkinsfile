pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // sh 'ls'
                // sh 'echo building...'

				// Retrieve DockerHub credentials by ID
                def dockerHubCredentials = credentials('DockerHub')
                    
                // Log in to DockerHub
				sh '''

                # Use docker login with your credentials
                docker login -u ${dockerHubCredentials.username} -p ${dockerHubCredentials.password}

				# build image
				docker build -t roberta:1.0-firstBuild .

				# tag image
				docker tag roberta:1.0-firstBuild firstRoberta

				#push image
				docker push roberta:1.0-firstBuild

				'''
            }
        }
    }
}