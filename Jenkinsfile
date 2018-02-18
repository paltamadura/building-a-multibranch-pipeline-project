node {
	withEnv(['CI=true']) {
		/* Requires the Docker Pipeline plugin to be installed */
	    docker.image('node:6-alpine').inside("-p 3000:3000 -p 5000:5000") {
	        stage('Build') {
	            sh 'npm install'
	        }
	        stage('Test') {
	            sh './jenkins/scripts/test.sh'
	        }
	        if (env.BRANCH_NAME == 'development') {
	        	stage('Deliver for development') {
	                sh './jenkins/scripts/deliver-for-development.sh'
	                input message: 'Finished using the web site? (Click "Proceed" to continue)'
	                sh './jenkins/scripts/kill.sh'
	            }
	        } else {
	        	sh "echo 'Branch is ${env.BRANCH_NAME}; Skipping Deliver for development'"
	        }
	        if (env.BRANCH_NAME == 'production') {
        		stage('Deploy for production') {
        			sh './jenkins/scripts/deploy-for-production.sh'
	                input message: 'Finished using the web site? (Click "Proceed" to continue)'
	                sh './jenkins/scripts/kill.sh'
        		}
        	} else {
	        	sh "echo 'Branch is ${env.BRANCH_NAME}; Skipping Deliver for production'"
	        }
		}
	}
}


