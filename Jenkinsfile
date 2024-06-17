pipeline{
    agent {
        label 'ansible-master'
    }
    stages{
        stage("check working directory"){
            steps{
                sh 'pwd'
                sh 'ls'
            }
        }
        stage("delete old artifact if exist"){
            steps{
                sh 'rm -rf *.zip || echo ""'
            }
        }

        stage("create zip file"){
            steps{
                sh 'wget https://github.com/teammy44u/ansible-jenkins/archive/refs/heads/main.zip'
            }
        }
         stage("Upload zip file in jfrog"){
            steps{
                sh 'curl -uadmin:AP8gcgmmset5jeYChTJYDN6XmDd \
                -T /home/ec2-user/jenkins/workspace/ansible-playbook \
                "http://ec2-3-86-7-150.compute-1.amazonaws.com:8081/artifactory/ansible-playbook/playbooks_${BUILD_ID}.zip"'
            }
        }
          stage("deliver playbooks on /home/ec2-user/ansible"){
            steps{
                sh 'mkdir -p /home/ec2-user/ansible'
                sh 'cp -f /home/ec2-user/jenkins/workspace/ansible-playbook/main.zip /home/ec2-user/ansible'
                sh '''
                cd /home/ec2-user/ansible
                unzip -o main.zip
                rm -f main.zip
                cp -rf ansible-jenkins-main/* .
                rm -rf ansible-jenkins-main/
                '''
            }
        }
        stage("check worker nodes connectivity"){
            steps{
                sh 'ansible all -m ping'
            }
        }
        stage("check test.yml"){
            steps{
                sh '''
                cd /home/ec2-user/ansible
                ansible-playbook test.yml --syntax-check
                '''
            }
        }

        stage("run playbook test.yml"){
            steps{
                sh 'ansible-playbook test.yml'
            }
        }


    }
}    
    
