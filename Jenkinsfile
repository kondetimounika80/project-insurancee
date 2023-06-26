node{
    stage('git checjout')
    {
        git branch: 'master', url: 'https://github.com/kondetimounika80/insure-me.git'
    }

    stage('build'){
    
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t kondetimounika/insureme:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'docker-password', variable: 'docker')]) {
        sh 'docker login -u kondetimounika -p ${docker}'
        sh 'docker push kondetimounika/insureme:1.0'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansiblekey', disableHostKeyChecking: true, installation: 'myAnsible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
