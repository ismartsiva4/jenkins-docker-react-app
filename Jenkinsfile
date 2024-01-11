node {   
    stage('Clone Github repository') {
        git branch: 'master', credentialsId: 'ismartsiva4', url: 'https://github.com/ismartsiva4/jenkins-docker-react-app.git'
    }
    
    stage('Build image') {
       dockerImage = docker.build("ismartsiva4/react-app")
    }
    
    stage('Push image') {
       withDockerRegistry([ credentialsId: "dockerhub-creds", url: "" ]) {
       dockerImage.push()
        }
    }    

    stage('Stop and Kill existing container with same name if any') {
        sh "docker rm -f react-app"
    }
        
    stage('Run the container Locally on the Jenkins server') {
        sh "docker run -itd --name react-app -p 80:80 ismartsiva4/react-app"
     
    }
  }
