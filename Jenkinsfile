pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the  webpage branch...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the webpage branch...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the webpage branch...'
                sh '''
                # Create the deployment directory
                mkdir -p /tmp/deployment_directory_webpage

                # Copy the signup.html file from the Jenkins workspace
                cp ${WORKSPACE}/Registration_Form/webpage.html /tmp/deployment_directory_webpage/

                # Start the Python HTTP server on port 9292
                nohup python3 -m http.server 9292 --directory /tmp/deployment_directory_webpage > /tmp/server_webpage.log 2>&1 &
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
