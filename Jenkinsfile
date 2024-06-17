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
    }
}    
    
