pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // sh 'ls'
                // sh 'echo building...'
				sh '''

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