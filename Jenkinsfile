  
def remote = [:]
  remote.name = 'Docker Server'
  remote.host = '18.222.179.121'
  remote.user = 'ubuntu'
  remote.password = 'popoola32'
  remote.allowAnyHosts = true

pipeline {
  agent any

  environment {
       imagename = "mayorpasca32/deployment"
       registryCredential = 'DOCKERLOGIN'
       dockerImage = ''
       imagetag    = "${env.BUILD_ID}"
           }

     stages {

          stage('Building Docker image') {
               steps{
                   script {
                       dockerImage = docker.build imagename
                          }
               }
          }

          stage('Push Image To DockerHub') {
               steps{
                     script {
                         docker.withRegistry( '', registryCredential ) {
                         //dockerImage.push("$BUILD_NUMBER")
                         dockerImage.push("$imagetag")
                                              }
                         }
               }
          }
          
          stage('SSH Test') {
               steps {
                    script {
                         sshCommand remote: 'remote', command: "docker run --name may-docker-class -d -p 9090:80 mayorpasca32/deployment:9"
                    }
               }
          }

          stage('Deploy To Docker Server Using SSH') {
               steps{
                    script {
                         sshCommand remote: remote, command: "docker run --name may-docker-class -d -p 9090:80 mayorpasca32/deployment:9"
                    }
               }
          }

          stage('Remove Unused docker image') {
               steps{
                    //sh "docker rmi $imagename:$BUILD_NUMBER"
                    //sh "docker rmi $imagename:$imagetag"
                    sh "docker system prune -f"
                    }
          }
    
     }
}
