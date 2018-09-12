node ('prod') {
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
             pwd 
             sh "hostname"
    }
    stage('Push Image') {
            docker.withRegistry('https://registry.hub.docker.com', 'f4fc89d0-de17-47ed-b9f4-ab5ebbe5cf39') {
            echo "${env.BUILD_NUMBER}"
            sh "docker tag saiprasad169/website-test saiprasad169/website-test:${env.BUILD_NUMBER} "
            sh "docker push saiprasad169/website-test:${env.BUILD_NUMBER}"
           }
   }
    stage('Deploy ') {  
        /*    sh " docker srevice create --name web -p 9089:80  linuxcloudops/website-test:${env.BUILD_NUMBER}"  */
         }
   }
