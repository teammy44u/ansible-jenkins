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
    }
}