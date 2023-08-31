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
                withCredentials([file(credentialsId: 'ansible-key', variable: 'ansibleKey')]) {
                    sh 'ls -la'
                    sh "cp /$ansibleKey ansibleKey"
                    sh 'cat ansibleKey'
                    sh 'ansible --version'
                    sh 'ls -la'
                    sh 'chmod 400 ansibleKey '
                    sh 'ansible-playbook -i hosts --private-key ansibleKey playbook.yml'
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
