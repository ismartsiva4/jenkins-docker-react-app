node {   
    stage('Clone Github repository') {
        git branch: 'master',
        git credentialsId: 'github-creds', url: 'https://github.com/ismartsiva4/jenkins-docker-react-app.git'
    }
    
    stage('Build image') {
       dockerImage = docker.build("cloudwithraghu/react-app:latest")
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
        sh "docker run -itd --name react-app -p 80:80 cloudwithraghu/react-app:latest"
     
    }
  }
