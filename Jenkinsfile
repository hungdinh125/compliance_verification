pipeline {
    agent any
    stages {
        stage('Clone the repository') {
            steps {
                git (branch: 'main',
                     url: 'https://github.com/hungdinh125/compliance_verification.git')
            }
        }
        stage('Verify the version and NTP configuration') {
            steps {
                sh 'ansible-playbook compliance_verification/compliance.yml -i compliance_verification/inventory --check'
            }
        }
    }
    post {
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true)
        }
    }
}
