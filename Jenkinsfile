node ('prod1') {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build images') {
        /* This builds the actual image; synonymous to
         * docker build on the command line. */
             sh "hostname"
             echo "${env.BUILD_NUMBER}"
             sh 'docker build -t saiprasad169/website-test -f webpage .'
             echo "${env.BUILD_NUMBER}"
             sh "docker tag saiprasad169/website-test saiprasad169/website-test:${env.BUILD_NUMBER} "
             pwd 
             sh "hostname"
    }
    stage('Push Image') {
            withDockerRegistry([ credentialsId: "fe6358bf-1056-440e-92f7-0f520af2dc59", url: "" ])
           /* docker.withRegistry('https://registry.hub.docker.com', 'bb0b7427-5db4-40b5-9361-310c3d163154') */ {
            echo "${env.BUILD_NUMBER}"
            sh "docker tag saiprasad169/website-test saiprasad169/website-test:${env.BUILD_NUMBER} "
            sh "docker push saiprasad169/website-test:${env.BUILD_NUMBER}"
           }
   }
    stage('Deploy ') {  
          /* sh " docker service create --name web -p 9089:80  saiprasad169/website-test:${env.BUILD_NUMBER}"  */
                    echo "saiprasad169/website-test:${env.BUILD_NUMBER}"
                     sh " sed -i 's/website-test/website-test:${env.BUILD_NUMBER}/g' docker-stack.yml"
                    sh "docker stack deploy -c docker-stack.yml website" 
         }
   }
