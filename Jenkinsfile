pipeline {
    agent any

    stages {
        stage('Initialize Terraform') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Apply Terraform') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }

        stage('Wait for Deployment') {
            steps {
                sleep 30
            }
        }

        stage('Run Ansible Playbook to install kubernetes') {
            steps {
                sh 'ansible-playbook -i /root/terraform/inventory.ini install_kubernetes.yaml'
            }
        }

        stage('Run Ansible Playbook to install Docker Compose Helm and argoCD') {
            steps {
                sh 'ansible-playbook -i /root/terraform/inventory.ini install_dc_helm_argocd.yaml'
            }
        }
    }
}
