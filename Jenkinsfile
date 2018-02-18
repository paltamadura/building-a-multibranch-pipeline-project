node {
	withEnv(['CI=true']) {
		/* Requires the Docker Pipeline plugin to be installed */
	    docker.image('node:6-alpine').withRun('-p 3000:3000 -p 5000:5000').inside {
	        stage('Build') {
	            sh 'npm install'
	        }
	        stage('Test') {
	            sh './jenkins/scripts/test.sh'
	        }
	    }
	}
}