pipeline {

    agent{
        docker {
            image 'khaliddinh/ansible'
        }
    }

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {

        stage('Deploy Mysql container') {
           
            steps {
                withCredentials([file(credentialsId: 'ansible-key', variable: 'ansible-key')]) {
                    sh 'ls -la'
                    sh "cp /$ansible-key ansible-key"
                    sh 'cat ansible-key'
                    sh 'ansible --version'
                    sh 'ls -la'
                    sh 'chmod 400 ansible-key '
                    sh 'ansible-playbook -i hosts --private-key ansible-key playbook.yml'
            }
            }
        }
        
    }
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }
}
