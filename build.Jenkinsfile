pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // sh 'ls'
                // sh 'echo building...'
				sh '''
				# Load the JSON secrets file
                def secrets = readJSON file: 'secrets.json'
                
                # Access specific secrets
                def dockerUsername = secrets.docker-credentials.username
                def dockerPassword = secrets.docker-credentials.password

                # Use docker login with your credentials
                docker login -u ${dockerUsername} -p ${dockerPassword}

				docker build -t roberta:1.0-firstBuild .
				docker tag roberta:1.0-firstBuild firstRoberta

				docker push roberta:1.0-firstBuild

				'''
            }
        }
    }
}