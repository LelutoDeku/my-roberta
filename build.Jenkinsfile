pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // sh 'ls'
                // sh 'echo building...'
				sh '''

				ls -l
				# Load the JSON secrets file
                secrets=$(cat secrets.json)

                # Extract specific secrets using jq (if available)
                dockerUsername=$(echo $secrets | jq -r '.docker.username')
                dockerPassword=$(echo $secrets | jq -r '.docker.password')

                # Use docker login with your credentials
                docker login -u ${dockerUsername} -p ${dockerPassword}

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