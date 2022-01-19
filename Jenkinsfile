node ('ubuntu-app-agent') {
  
    def app

    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */

       checkout scm
    }
     
    stage('Build-and-Tag') {
      
     // sh 'echo Build-and-Tag'
        /* This builds the actual image; synonymous to
         * docker build on the command line */

      app = docker.build("multanid/snake")
    }
  
  stage('Post-to-dockerhub') {
    
    sh 'echo Post-to-dockerhub'
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
      docker.withRegistry('https://registry.hub.docker.com', 'docker') {
      app.push("latest") 
     
      }
         }

    stage('Pull-image-server') {
      
      sh "docker-compose down"
      sh "docker-compose up -d"			
      }
   
}
