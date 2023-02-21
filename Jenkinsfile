pipeline {
        agent any
      /*  environement{

            DOCKERHUB_CREDENTIALS=credentials('dockerhub')
        }*/

    stages {
    
        stage('git clone') {
                steps {
                     git branch: 'main', credentialsId: 'jenkins', url: 'git@gitlab.com:Aguerbaoui/project-9.git'
            
            
                }
        
        }

        stage('Build') {
                steps {
                     withMaven(maven: 'Maven') {
                    sh script: 'mvn clean install package'}
        
                }
        }

        stage('Docker Build and Tag') {
           steps {
            sh 'docker build -t nadiaaguerbaoui1/tomcat-image:latest .'
           
               }
        }
     
         stage('Publish image to Docker Hub') {
          
            steps {
                withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                   
                   sh 'docker push nadiaaguerbaoui1/tomcat-image:latest'
                   }
      
                  
          }
        }

        stage('Ansible Playbook')
        {

            steps{
                 ansiblePlaybook credentialsId: 'private_key1', installation: 'ansible', inventory: 'ansible/inventory/hosts', playbook: 'ansible/playbooks/playbook.yml'

            }
        }
         


     /* stage('Deploy to k8s cluster'){
        steps{

            script{
                   // kubernetesDeploy (configs: 'dep.yaml', kubeconfigId: 'kubeconfig')
                    kubernetesDeploy configs: 'deployservice.yaml', kubeConfig: [path: ''], kubeconfigId: 'kubeconfig', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
                }

         }


     }   */


  
     

    } 

} 
