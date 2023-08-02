node{

        stage('git checkout'){
                checkout scm
        //     echo "checking out the code from github"
        //     git 'https://github.com/ggadde4/insurance-project.git'
        }
        
        stage('maven build'){
                echo 'starting maven build'
                sh 'mvn clean package'
                sh 'ls -altr'
                sh 'cd target/ && pwd && ls -altrh && cd .. && pwd'
        }
        
        
        stage('build docker image'){
            sh 'docker build -t gg04/insure-me:1.0 .'
            sh 'docker images'
        }
        
        stage('push docker image to docker hub registry'){
            echo 'pushing images to registry'
            withCredentials([string(credentialsId: 'DockerPWD', variable: 'dockerHubPassword')]) {
                sh "docker login -u gg04 -p ${dockerHubPassword}"
                sh 'docker push gg04/insure-me:1.0'
            }
        }
        
        /*stage('configure test-server and deploy insure-me'){
            echo "configuring test-server"
          //  sh 'ansible-playbook configure-test-server.yml'
            ansiblePlaybook become: true, credentialsId: 'ssh-key-ansibles', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml'
        }*/
        
}
