pipeline {
    agent any
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/sunnnyyk/access-cluster.git', branch: 'main'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                withCredentials([
                    string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'aws_access_key'),
                    string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'aws_secret_key')
                ]) {
                    sh '''
                        ansible-playbook -i inventory.ini install_kubectl_and_kubeconfig.yml \
                        -e "aws_access_key=${aws_access_key} aws_secret_key=${aws_secret_key}"
                    '''
                }
            }
        }
    }

}
