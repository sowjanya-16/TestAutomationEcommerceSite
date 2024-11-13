pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Generate SBOM with cdxgen') {
            steps {
                echo 'Generating SBOM using cdxgen...'
                // Run cdxgen to create the SBOM in CycloneDX format
                sh '/usr/local/bin/cdxgen -o sbom.json'
                archiveArtifacts artifacts: 'sbom.json', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            //cleanWs()  // Clean up the workspace after the build
        }
        success {
            echo 'SBOM generation completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
