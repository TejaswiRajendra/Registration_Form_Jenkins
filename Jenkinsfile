pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the webApp branch...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the webApp branch...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the webApp...'
                sh '''
                # Create the deployment directory
                mkdir -p /tmp/deployment_directory_webApp

                # Check if login.html exists
                if [ ! -f ${WORKSPACE}/webApp.html ]; then
                    echo "Error: webApp.html not found in workspace."
                    exit 1
                fi

                # Copy the login.html file from the Jenkins workspace
                cp ${WORKSPACE}/webApp.html /tmp/deployment_directory_webApp/

                # Start the Python HTTP server on port 9191
                nohup python3 -m http.server 9191 --directory /tmp/deployment_directory_webApp > /tmp/server_webApp.log 2>&1 &
                '''
                echo "webApp is being served on http://localhost:9191"
            }
        }
        stage('Archive HTML') {
            steps {
                archiveArtifacts artifacts: '*.html', fingerprint: true
            }
        }
    }
}
