pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // sh 'ls'
                // sh 'echo building...'
				sh '''
				# Load the JSON secrets file
                secrets=$(cat secrets.json)

                # Extract specific secrets using jq (if available)
                dockerUsername=$(echo $secrets | jq -r '.docker.username')
                dockerPassword=$(echo $secrets | jq -r '.docker.password')

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