pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo '📥 Checking out source code'
                checkout scm
            }
        }

        stage('Install Ansible (if not present)') {
            steps {
                sh '''
                if ! command -v ansible >/dev/null 2>&1; then
                  echo "🔧 Installing Ansible"
                  apt-get update
                  apt-get install -y ansible
                else
                  echo "✅ Ansible already installed"
                fi
                '''
            }
        }

        stage('Verify Ansible') {
            steps {
                sh '''
                echo "🔍 Ansible version"
                ansible --version
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                echo "🚀 Running Ansible playbook"
                cd ansible
                ansible-playbook -i inventory.ini playbook.yml
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully'
        }
        failure {
            echo '❌ Deployment failed'
        }
    }
}
