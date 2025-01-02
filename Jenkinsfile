pipeline {
    agent any
    options {
        disableConcurrentBuilds()
        cleanWs()
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the master branch...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the master branch...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the master branch...'
                sh '''
                # Debugging: List workspace content
                echo "Workspace content:"
                ls -l ${WORKSPACE}

                echo "Registration_Form directory content:"
                ls -l ${WORKSPACE}/Registration_Form/

                # Ensure the Form.html file exists
                if [ ! -f "${WORKSPACE}/Registration_Form/Form.html" ]; then
                    echo "Form.html not found. Deployment cannot proceed."
                    exit 1
                fi

                # Create the deployment directory
                mkdir -p /tmp/deployment_directory_master

                # Copy the Form.html file
                cp ${WORKSPACE}/Registration_Form/Form.html /tmp/deployment_directory_master/

                # Start the Python HTTP server
                if ! command -v python3 > /dev/null; then
                    echo "Python3 is not installed or not in PATH."
                    exit 1
                fi

                if lsof -i:9090 > /dev/null; then
                    echo "Port 9090 is already in use."
                    exit 1
                fi

                nohup python3 -m http.server 9090 --directory /tmp/deployment_directory_master > /tmp/server_master.log 2>&1 &
                echo "Python HTTP server started."
                '''
                echo "Form is being served on http://localhost:9090"
            }
        }
        stage('Archive HTML') {
            steps {
                script {
                    def htmlFiles = sh(script: "find . -name '*.html'", returnStdout: true).trim()
                    if (!htmlFiles) {
                        error("No HTML files found to archive.")
                    }
                }
                archiveArtifacts artifacts: '*.html', fingerprint: true
            }
        }
    }
}

