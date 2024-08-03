pipeline {
    agent any
    stages {
        stage('Clone the repository') {
            steps {
                git (branch: 'main',
                     url: 'https://github.com/hungdinh125/compliance_verification.git')
            }
        }
        stage('Verify directory is cloned') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Verify reachability') {
            steps {
                build(job: 'reachability_check')
            }
        }
        stage('Verify the version and NTP configuration') {
            steps {
                sh 'ansible-playbook compliance.yml -i inventory --check'
            }
            post {
                failure {
                    sh 'ansible-playbook compliance.yml -i inventory'
                }
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
