pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the webpage branch...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the webpage branch...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the webpage...'
                sh '''
                # Create the deployment directory
                mkdir -p /tmp/deployment_directory_webpage

                # Check if webpage.html exists
                if [ ! -f ${WORKSPACE}/webpage.html ]; then
                    echo "Error: webpage.html not found in workspace."
                    exit 1
                fi

                # Copy the webpage.html file from the Jenkins workspace
                cp ${WORKSPACE}/webpage.html /tmp/deployment_directory_webpage/

                # Start the Python HTTP server on port 9292
                nohup python3 -m http.server 9292--directory /tmp/deployment_directory_webpage > /tmp/server_webpage.log 2>&1 &
                '''
                echo "webpage is being served on http://localhost:9292"
            }
        }
        stage('Archive HTML') {
            steps {
                archiveArtifacts artifacts: '*.html', fingerprint: true
            }
        }
    }
}
