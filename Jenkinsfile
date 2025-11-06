pipeline {
    agent any

    tools {
        nodejs 'Node'  // Make sure to have NodeJS installed in Jenkins
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Code Quality Check') {
            steps {
                script {
                    try {
                        sh 'npm run lint'
                        currentBuild.result = 'SUCCESS'
                        setBadgeStatus('PASS')
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        setBadgeStatus('FAIL')
                        error('Code quality check failed')
                    }
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Pipeline Status: ${currentBuild.fullDisplayName}",
                body: """Code Quality Check Results:
                Status: ${currentBuild.result}
                Details: ${env.BUILD_URL}""",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
    }
}

def setBadgeStatus(String status) {
    sh """
        echo '{"schemaVersion": 1, "label": "quality", "message": "${status}", "color": "${status == 'PASS' ? 'success' : 'critical'}"}' > quality-badge.json
    """
    // You'll need to configure your CI to host this JSON file for badge generation
}